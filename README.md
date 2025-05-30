# MangoODM

**MangoODM** — lightweight and easy-to-use ODM (Object Document Mapper) library for Python, designed to work asynchronously with MongoDB using the `motor` driver.  
Supports Pydantic models and MongoDB sessions.

---

## Features

- Simple model definition using Pydantic  
- Model registration and automatic collection handling  
- Asynchronous CRUD operations: insert, find, update, delete  
- Support for MongoDB sessions for transaction safety  
- Logging for important events and errors

---

## Installation

```
pip install mangodb.py
```

## Usage

### Define your model

```python 

from mango impot MangoModel

class GDBeach(MangoModel):
    name: str
    role: str

```

### Initialize ODM and register model

```python

import asyncio
from motor.motor_asyncio import AsyncIOMotorClient
from mango import MangoODM, MangoModel

class GDBeach(MangoModel):
    name: str
    role: str

async def main():

    client = AsyncIOMotorClient("mongodb://localhost:27017") # you also can use srv
    db = client["MangoDB"]
    odm = MangoODM(db)
    odm.register_model(GDBeach)

    async with await client.start_session() as session:

        insert_result = await odm.insert_one("GDBeach", session=session, name="xSodium", role="soda")
        print(f"Inserted document ID: {insert_result.inserted_id}")

        found_doc = await odm.find_one("GDBeach", session=session, name="xSodium")
        print(f"Found document: {found_doc}")

asyncio.run(main())

```

# that's all!
