# Fine-tuning

The goal of the second part of the school project for the subject ADSDB (Algorithms, Data Structures, and Databases) is to leverage the pipeline developed in the first part to generate training data for fine-tuning an embedding-generation model. For this purpose, we will use the repository created in the previous work as a baseline and continue following a structured workflow, progressing from training data construction to model fine-tuning in layered zones, similar to the approach used earlier.

---

## First Steps

### Working Environment for Notebooks

- Open a terminal and start the Jupyter Notebook framework:
```bash
jupyter notebook
```
- Execute the notebooks in your browser.

---

### Start Docker Containers

Open Docker Desktop and launch the following containers:

#### MinIO
```bash
docker run -d --name minio \
  -p 9000:9000 -p 9001:9001 \
  -e MINIO_ROOT_USER=minioadmin \
  -e MINIO_ROOT_PASSWORD=minioadmin \
  -v C:\minio\data:/data \
  minio/minio server /data --console-address ":9001"
```
- After the container has been initialized, the MinIO Web UI can be accessed at [http://127.0.0.1:9001](http://127.0.0.1:9001) Furthermore, starting from the **Persistent_Landing** stage, the data were organized into three subfolders, texts,images, and videos, each corresponding to the different data formats we used. Here, we also created a volume on the local machine. Since MinIO's storage is limited, we could previously store only a few files there.

#### ChromaDB
```bash
docker run -d --name chroma \
  -p 8000:8000 \
  -e PERSIST_DIRECTORY=/chroma/chroma \
  -v C:\chromadb\exploitation-zone:/chroma/chroma \
  chromadb/chroma:latest
```
- In this configuration, we explicitly define a persistent storage path for ChromaDB to store its embeddings outside the container. However, during experimentation, it was observed that ChromaDB tends to store the embeddings internally within the container, regardless of the external volume path. This behavior may vary depending on the ChromaDB version and container configuration of the device.

---

## Execution Order

### Landing Zone
- `landing_zone.ipynb`  
- `temporal_landing.ipynb`  
- `persistent_landing.ipynb`  

### Formatted Zone
- `formatted_zone.ipynb`  
- `formatted_zone_homogenizer_texts.ipynb`  
- `formatted_zone_homogenizer_images.ipynb` 

### Trusted Zone
- `trusted_zone.ipynb`  
- `trusted_zone_text_quality_processes.ipynb`
- `trusted_zone_image_quality_processes.ipynb`

### Exploitation Zone
- `exploitation_zone_text_embeddings.ipynb`
- `exploitation_zone_image_embeddings.ipynb`
- `exploitation_zone_text_image_embeddings.ipynb`

### Training Data Construction Zone
- `baseline training data generation.ipynb`
- `image augmented training data generation.ipynb`
- `text augmented training data generation.ipynb`
- `text image augmented training data generation.ipynb`

### Training Zone
- `training zone.ipynb`
- `training FP16-INT4.ipynb`
- `training LoRA.ipynb`
- `training FP16-INT4-LoRA.ipynb`

### Test Zone
- `test data preparation.ipynb`
- `Quantized model evaluation.ipynb`
- `LoRA model evaluation.ipynb`
- `Q LoRA model evaluation.ipynb`

> Follow this order so that data flows correctly from ingestion to exploitation while maintaining the layered structure.

## Notes

- Each notebook corresponds to a specific stage in the pipeline.

