# DentifyX-BE-Manual

## **Prerequisites**
- `python 3.7 or later` installed

## **Build** (local)
1. Inside a project directory, run install necessary python package
    ```
        pip install -r requirements.txt
    ```
2. Create `.env` file with following contents:
    ```Dotenv
        ADMIN_TOKEN="" # any string used as super admin key to bypass all validation (for testing purpose)
        APP_STATE="dev" # app state ("dev" - enable all debugging | "prod" - disable all debugging)

        CONNECTION_STRING="" # connection string of MongoDB Atlas
        DATABASE_NAME="DentifyX" # name of used database / collection
        
        MODELS_KEY="" # Machine learning access key for getting predictions (Might not required for Local ML Server)
        MODELS_URL="" # Machine learning endpoints for getting predictions

        PREDICT_CLASSES='{"Angulation": false, "Depth": false, "Ramus_Relationship": false, "Difficulty": true}' # String of object indicates considered criterior
        SECRET_KEY="" # secret key for jwt token signature
        TOKEN_EXP_TIME=9000 # jwt token lifespan
    ```
    > NOTE: This `.env` file require 2 external services:  
        - Cloud Database > [MongoDB Atlas](https://www.mongodb.com/atlas/database)  
        - ML Server > [Azure ML service](https://azure.microsoft.com/en-au/products/machine-learning) **OR** Local ML Server (refer to [this installation](#machine-learning-server))


## **Run** (local)
Excecute following command to run DentifyX backend in local
```
    python app.py
```
OR
```
    python3 app.py
```

##  **Usage**
Check `DentifyX_API_docs.pdf` inside `docs` directory

## **Machine Learning Server**
There are 2 ways to create ML server for backend  
1. Using external service - [Azure ML](https://azure.microsoft.com/en-au/products/machine-learning)
2. Create Local Machine Learning Server (Not recommended)

### **Local Machine Learning Server Setup**
1. Create a server using `flask` (Can use this project as a reference) or any preferred frameworks
2. Implement API for obtain model predictions
    > NOTE: Please refer to `MLEntryScript` to see how model was inferenced and how each API handle the request and response data
3. Change following environment variables in `.env` file ([Build section](#build-local) step 2):
    ```Dotenv
       MODELS_KEY="<your-local-ml-key>" # if have no key, leave it as an empty string
       MODELS_URL="<your-local-ml-url-endpoints>" 
    ```