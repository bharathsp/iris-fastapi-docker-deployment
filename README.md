# 🌸 ML Model Deployment using FastAPI & Docker (Iris Dataset)

This project demonstrates how to **train, deploy, and consume a machine learning model** using **FastAPI** 🚀 and **Docker** 🐳.
The model predicts **Iris flower species** based on input features:

* 🌱 **Sepal Length**
* 🌱 **Sepal Width**
* 🌸 **Petal Length**
* 🌸 **Petal Width**

---

## 🎯 Goal

* Train a **Random Forest Classifier** to classify iris flower species.
* Save the trained model into a `.joblib` file.
* Expose the model via **REST APIs** built using **FastAPI**.
* Containerize the application with **Docker** for easy deployment.

---

## 🛠️ Tools & Technologies

* **Machine Learning:** Random Forest Classifier 🌳
* **API Framework:** FastAPI ⚡
* **Server:** Uvicorn 🔌
* **Containerization:** Docker 🐳
* **Dataset:** Iris dataset 🌸

---

## 📂 Project Structure

```
├── app/
│   ├── server.py       # FastAPI app (GET & POST endpoints)
│   ├── model.joblib    # Saved ML model
│
├── client.py           # Script to automate predictions
├── requirements.txt    # Required dependencies
├── Dockerfile          # Docker build instructions
└── README.md           # Project documentation
```

---

## ⚙️ Steps to Implement

### 1. 📊 Train the Model

* Train a **Random Forest Classifier** on the Iris dataset.
* Save the trained model as `model.joblib` using `joblib.dump()`.

<img width="412" height="276" alt="image" src="https://github.com/user-attachments/assets/741e301d-6836-4f1a-a2e4-ad0d43a026d8" />

*joblib_file_creator.ipynb*

---

### 2. 🖥️ Build the API

* Create `server.py` with FastAPI.
* Load the saved model.
* Implement:

  * ✅ **GET endpoint** → simple health check / welcome message.
  * ✅ **POST endpoint** → accepts flower features & returns predicted species.

<img width="542" height="572" alt="image" src="https://github.com/user-attachments/assets/bd26f752-db7c-4c81-9bdb-8e6b1331ccf5" />

*server.py*

---

### 3. 📦 Requirements

Create a `requirements.txt` with all dependencies:

```
fastapi
uvicorn
scikit-learn
joblib
```

---

### 4. 🐳 Docker Setup

**Dockerfile Overview:**

1. Base image → `FROM python:3.11` 🐍
2. Create working directory → `WORKDIR /code`
3. Copy and install dependencies → `requirements.txt`
4. Copy app files into container.
5. Expose port `8000` 🌐
6. Run FastAPI app with Uvicorn:

   ```
   CMD ["uvicorn", "app.server:app", "--host", "0.0.0.0", "--port", "8000"]
   ```

This line goes into your **Dockerfile** and tells Docker **what command to run when the container starts**.

---

#### 🔎 Breakdown

1. **`CMD`**

   * In Docker, `CMD` defines the **default command** that will be executed when a container starts.
   * If you don’t override it when running `docker run`, this is what executes.

---

2. **`uvicorn`**

   * Uvicorn is an **ASGI (Asynchronous Server Gateway Interface) server**.
   * It runs the FastAPI application and handles incoming HTTP requests.
   * Think of it as the “engine” powering your API.

---

3. **`app.server:app`**

   * This tells Uvicorn **where to find the FastAPI app**.
   * Format: `module_name:variable_name`

     * `app.server` → Python file/module path (here, `server.py` inside the `app` folder).
     * `app` → The FastAPI application instance defined in that file, usually something like:

       ```python
       from fastapi import FastAPI
       app = FastAPI()
       ```
   * Together, `app.server:app` means:
     *“Go to `server.py` inside the `app` folder, and use the FastAPI app object named `app`.”*

---

4. **`--host 0.0.0.0`**

   * By default, Uvicorn binds only to `127.0.0.1` (localhost), which is accessible only inside the container.
   * `0.0.0.0` means **listen on all network interfaces**, making the API accessible from outside the container.
   * This is crucial in Docker, otherwise you couldn’t access the API from your machine.

---

5. **`--port 8000`**

   * Specifies the port inside the container on which the FastAPI app will run.
   * Here, it’s running on port **8000**.
   * When running Docker, you map it to your host using `-p 8000:8000`.

---

<img width="573" height="254" alt="image" src="https://github.com/user-attachments/assets/c43db7bd-8f1c-4adb-84c2-48dfeee0bdf6" />

*Dockerfile*

---

### 5. 🔨 Build & Run Docker

* Build image:

  ```bash
  docker build -t iris-fastapi .
  ```
  
  <img width="1919" height="416" alt="image" src="https://github.com/user-attachments/assets/7696165f-b4d3-4d80-9a94-9a3f1da5176f" />

* Run container:

  ```bash
  docker run -p 8000:8000 iris-fastapi
  ```
<img width="715" height="98" alt="image" src="https://github.com/user-attachments/assets/287de618-ecaf-47dd-b859-3f8e47696b20" />

---

### 6. 🌍 Access the API

* Uvicorn runs the server at:
  👉 [http://0.0.0.0:8000](http://0.0.0.0:8000)

* FastAPI docs available at:
  👉 [http://0.0.0.0:8000/docs](http://0.0.0.0:8000/docs)

Here you can test the **POST API** by sending flower feature inputs.

**Example Request (POST):**

```json
{
  "features": [5.1, 3.5, 1.4, 0.2]
}
```

**Example Response:**

```json
{
  "prediction": "setosa"
}
```

---

### 7. 🤖 Automating Predictions

Use `client.py` to send multiple flower features in bulk.
The script loops through the input list, sends requests to the API, and prints predictions automatically.

---

## 🧪 Testing the Workflow

1. Run the Docker container.
2. Open [http://0.0.0.0:8000/docs](http://0.0.0.0:8000/docs).
3. Try out the endpoints:

   * GET → Health check.
   * POST → Send flower features → Get species prediction.
4. Run `client.py` for batch predictions.

---

## 📌 Key Notes

* Port `8000` must be exposed for API access.
* Docker ensures the app runs in an **isolated environment**.
* FastAPI auto-generates **interactive API docs** ✨.

---

## 🚀 Future Enhancements

* Add CI/CD pipeline for deployment.
* Deploy to cloud (AWS/GCP/Azure).
* Extend to handle more datasets & models.

---

### 💡 Quick Start

1. Clone repo → `git clone <repo_url>`
2. Build Docker image → `docker build -t iris-fastapi .`
3. Run → `docker run -p 8000:8000 iris-fastapi`
4. Test at → [http://0.0.0.0:8000/docs](http://0.0.0.0:8000/docs)

🌸 Enjoy predicting Iris flowers with ML + FastAPI + Docker!
