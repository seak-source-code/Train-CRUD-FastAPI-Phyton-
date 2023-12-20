# Train-CRUD-FastAPI-Phyton- How to Create CRUD Operations with FastAPI 

# Step 1: Install FastAPI
pip install fastapi

# Step 2: Create a FastAPI Application
from fastapi import FastAPI
from pydantic import BaseModel
from typing import List

app = FastAPI()

# Step 3: Define Data Models:

class Item(BaseModel):
    id: int
    name: str
    price: float

# Step 4: Create CRUD Routes and Handlers

items = []

@app.get("/items", response_model=List[Item])
async def read_items():
    return items

@app.post("/items", response_model=Item)
async def create_item(item: Item):
    items.append(item)
    return item

@app.put("/items/{item_id}", response_model=Item)
async def update_item(item_id: int, item: Item):
    items[item_id] = item
    return item

@app.delete("/items/{item_id}")
async def delete_item(item_id: int):
    del items[item_id]
    return {"message": "Item deleted"
# Step 5: Run the Application
uvicorn main:app --reload

# Step 6: Test CRUD Operation

# 1. Create a new item: Send a POST
POST http://localhost:8000/items
{
    "id": 1,
    "name": "Apple",
    "price": 0.5
}

# 2. Get all items: Send a GET request
GET http://localhost:8000/items

# 3. Update an item: Send a PUT
PUT http://localhost:8000/items/0
{
    "id": 1,
    "name": "Orange",
    "price": 0.5
}

# 4. Delete an item: Send a DELETE request to delete an item.
DELETE http://localhost:8000/items/1




