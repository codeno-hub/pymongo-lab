!pip install pymongo
from pymongo import MongoClient

url = ""
client = MongoClient(url)

db = client['techgear_db']
orders_col = db['orders']
customers_col = db['customers']

orders_col.delete_many({})
customers_col.delete_many({})

store_orders = [
    {"order_id": 101, "customer_id": "C1", "status": "shipped", "items": ["laptop", "mouse"], "total": 1250},
    {"order_id": 102, "customer_id": "C2", "status": "shipped", "items": ["keyboard", "mouse"], "total": 110},
    {"order_id": 103, "customer_id": "C1", "status": "shipped", "items": ["monitor", "hdmi cable"], "total": 350},
    {"order_id": 104, "customer_id": "C3", "status": "pending", "items": ["mousepad", "mouse"], "total": 40},
    {"order_id": 105, "customer_id": "C2", "status": "shipped", "items": ["laptop", "webcam"], "total": 1260}
]

store_customers = [
    {"customer_id": "C1", "name": "Amit", "city": "Mumbai", "tier": "Gold"},
    {"customer_id": "C2", "name": "Priya", "city": "Bengaluru", "tier": "Silver"},
    {"customer_id": "C3", "name": "Rahul", "city": "Delhi", "tier": "Bronze"}
]

orders_col.insert_many(store_orders)
customers_col.insert_many(store_customers)
print("Both collections loaded successfully!")

#unpacking the arraya($unwind)
pipeline= [
    {"$unwind":"$items"}
]

for doc in orders_col.aggregate(pipeline):
    print(f"Order{doc['order_id']} -> Item: {doc['items']}")

pipeline= [
    {"$unwind":"$items"},
    {
        "$group":{
            "_id":"$items",
            "times_sold":{"$sum":1}
        }},
    {"$sort":{"times_sold":-1}}
]

for doc in orders_col.aggregate(pipeline):
    print(f"Item: {doc['_id']} -> Times Sold: {doc['times_sold']}")

#$project
pipeline = [
    {"$match": {"status": "shipped"}},

    {
        "$project":{
            "_id": 0,
            "order_id": 1,
            "subtotal": "$total",
            "With_tax": {"$multiply": ["$total", 1.18]}
        }
    }
]

for invoice in orders_col.aggregate(pipeline):
    print(f"Order: {invoice['order_id']} -> Subtotal: {invoice['subtotal']} -> With Tax: {invoice['With_tax']}")

#$lookup --> left join
pipeline = [
    {
        "$lookup": {
            "from": "customers",
            "localField": "customer_id",
            "foreignField": "customer_id",
            "as": "customer_details"
        }
    }
]

for orders in orders_col.aggregate(pipeline):
    print(f"Order {orders['order_id']} Total: ${orders['total']} Customer: {orders['customer_details']}")

#collscan
#IXSCAN
orders_col.drop_indexes()

before = orders_col.find({"customer_id": "C1"}).explain()["executionStats"]
print(f"Before: {before['totalDocsExamined']}")

orders_col.create_index("customer_id")

after = orders_col.find({"customer_id": "C1"}).explain()["executionStats"]
print(f"after: {after['totalDocsExamined']}")
