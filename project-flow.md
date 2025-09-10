### ## 📂 Recommended Datasets (Choose One)

For a project using a brute-force search with MySQL, you should start with a dataset that is large enough to be interesting but not so massive that it becomes too slow.

1.  **[Kaggle Fashion Product Images Dataset](https://www.kaggle.com/datasets/paramaggarwal/fashion-product-images-dataset)**: (Approx. 44k images) - **Highly Recommended**. The visual results are very intuitive (e.g., finding similar t-shirts or shoes).
2.  **[Caltech-101](https://data.caltech.edu/records/20086)**: (Approx. 9k images) - A classic dataset with 101 object categories. Great for learning.
3.  **[CIFAR-100](https://www.cs.toronto.edu/~kriz/cifar.html)**: (60k images) - Another classic. The images are small (32x32), which makes the embedding generation process very fast.

---

### ## 🛠️ Required Skills List (MySQL Focus)

#### 1. Core Machine Learning Concepts
* **Transfer Learning**: Understanding how to use a pre-trained model (like ResNet50) to extract features without training it yourself.
* **Embeddings**: Knowing that an embedding is a numerical vector that represents an object (like an image).
* **Similarity Metrics**: Understanding and being able to implement **Cosine Similarity** to measure how "close" two vectors are.
* **k-Nearest Neighbors (k-NN)**: The concept of finding the 'k' most similar items from a dataset based on a distance metric.

#### 2. Python & Libraries
* **`torch` & `torchvision`**: To load the pre-trained ResNet50 model and generate embeddings.
* **`Pillow` (PIL)**: For all image loading and preprocessing tasks.
* **`numpy`**: For efficient numerical operations on the vectors.
* **`mysql-connector-python`**: The official driver to connect your Python application to your MySQL database.
* **`boto3`**: (If using S3) The AWS SDK to interact with your S3 bucket.

#### 3. Database Skills (MySQL)
* **Basic SQL**: `CREATE TABLE`, `INSERT`, `SELECT`.
* **MySQL Data Types**: Knowing how to use `TEXT` or `JSON` to store the list of numbers that make up your vector.
* **MySQL Administration**: Setting up the database, creating a user, and getting the connection credentials.

#### 4. Cloud Skills (AWS)
* **Amazon RDS for MySQL**: Launching, configuring, and managing a managed MySQL instance.
* **Amazon S3**: Storing your image dataset in the cloud.
* **IAM Role**: Giving your compute environment (EC2/SageMaker) secure permission to access S3.
* **EC2 or SageMaker**: A working knowledge of using a cloud-based machine to run your scripts.

---

### ## 🗺️ The 4-Week Project Roadmap

#### **Week 1: Foundations & Infrastructure Setup**
* **Goal**: Get your environment ready and solidify your understanding.
* **Tasks**:
    1.  Choose and download one of the recommended datasets.
    2.  Set up your AWS account. Launch an **Amazon RDS for MySQL** instance. Note down the credentials.
    3.  Create an **S3 bucket** and upload your chosen dataset to it.
    4.  Set up your Python environment (on your local machine or an EC2 instance) and install all the required libraries.
    5.  Write a simple Python script that successfully connects to your RDS database.
    6.  Create the `images` table in MySQL with columns for `id`, `image_path`, and `embedding` (using the `TEXT` or `JSON` type).

#### **Week 2: Data Processing and Embedding Generation**
* **Goal**: Process all your images and populate the database.
* **Tasks**:
    1.  Write the core Python script that will be the "ETL" (Extract, Transform, Load) pipeline.
    2.  **Extract**: The script should list all image paths from your S3 bucket.
    3.  **Transform**: For each image path, the script will:
        * Load the image using Pillow.
        * Preprocess it for the ResNet50 model.
        * Use the loaded PyTorch model to generate the embedding vector.
    4.  **Load**: Insert the image's path and its embedding (converted to a string or JSON) into your MySQL table.
    5.  Run this script for your entire dataset. This might take some time!

#### **Week 3: Implementing the Brute-Force Search Logic**
* **Goal**: Build the core functionality of the search engine.
* **Tasks**:
    1.  Write a new Python script or function called `find_similar_images()`.
    2.  This function will take a path to a query image as input.
    3.  It will generate the embedding for this query image using the same process as Week 2.
    4.  It will then connect to MySQL and execute `SELECT image_path, embedding FROM images;` to fetch **all** records.
    5.  In your Python code, you will loop through every embedding from the database, calculate its cosine similarity with the query embedding, and store the results.
    6.  Sort the results by similarity score and return the top 5-10 image paths.

#### **Week 4: Building an API & Project Documentation**
* **Goal**: Make your project accessible and ready to showcase.
* **Tasks**:
    1.  **(Recommended)** Wrap your search function in a simple web API using **Flask** or **FastAPI**. This allows you to create an endpoint where a user can submit an image and get a JSON response with the similar image URLs.
    2.  Create a **GitHub repository** for your project.
    3.  Write a detailed `README.md` file. This is crucial.
        * Describe the project's goal.
        * Explain the architecture (S3 for storage, RDS for database, Python for logic).
        * **Discuss the scalability limitations**: Explicitly state that you used a brute-force search with MySQL and explain how you would re-architect it for a larger scale (mentioning PostgreSQL with `pgvector` or a dedicated vector DB).

