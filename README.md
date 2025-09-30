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

---

### 2. 🖥️ Build the API

* Create `server.py` with FastAPI.
* Load the saved model.
* Implement:

  * ✅ **GET endpoint** → simple health check / welcome message.
  * ✅ **POST endpoint** → accepts flower features & returns predicted species.

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

---

### 5. 🔨 Build & Run Docker

* Build image:

  ```bash
  docker build -t iris-fastapi .
  ```
* Run container:

  ```bash
  docker run -p 8000:8000 iris-fastapi
  ```

---

### 6. 🌍 Access the API

* Uvicorn runs the server at:
  👉 [http://127.0.0.1:8000](http://127.0.0.1:8000)

* FastAPI docs available at:
  👉 [http://127.0.0.1:8000/docs](http://127.0.0.1:8000/docs)

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
2. Open [http://127.0.0.1:8000/docs](http://127.0.0.1:8000/docs).
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
4. Test at → [http://127.0.0.1:8000/docs](http://127.0.0.1:8000/docs)

🌸 Enjoy predicting Iris flowers with ML + FastAPI + Docker!
