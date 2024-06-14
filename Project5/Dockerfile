# apt-get update && apt-get upgrade 
# apt-get install -y wget python3
# apt-get install -y python3-pip



# Use Ubuntu 20.04 as base image
FROM ubuntu:20.04

# Print a message before installing necessary packages
RUN echo "Installing necessary packages..."

# Install necessary packages
RUN apt-get update && \
    apt-get install -y wget bzip2 unzip && \
    apt-get clean

# Print a message before downloading and installing Miniconda3
RUN echo "Downloading and installing Miniconda3..."

# Download and install Miniconda3 suitable for ARM architecture (Apple M1)
RUN wget https://repo.anaconda.com/miniconda/Miniconda3-4.10.3-Linux-arm64.sh -O /tmp/miniconda.sh && \
    bash /tmp/miniconda.sh -b -p /opt/miniconda && \
    rm /tmp/miniconda.sh

# Print a message before adding Miniconda3 to PATH
RUN echo "Adding Miniconda3 to PATH..."

# Add Miniconda3 to PATH
ENV PATH /opt/miniconda/bin:$PATH

# Print a message before creating a new Conda environment
RUN echo "Creating a new Conda environment..."

# Create a new Conda environment
RUN conda install -y python=3.4.4 && \
    conda install -y biopython=1.68 matplotlib=1.5.1 numpy=1.11.3 pandas=0.18.1 scikit-learn=0.18.1 && \
    conda clean -ya

# Download GitHub repository and unzip
RUN wget https://github.com/ShiuLab/ML-Pipeline/archive/refs/heads/master.zip -O /tmp/ml_pipeline.zip && \
    unzip /tmp/ml_pipeline.zip -d /tmp && \
    rm /tmp/ml_pipeline.zip

# Set working directory to the downloaded repository
WORKDIR /tmp/ML-Pipeline-master

# Clean data
RUN echo "Cleaning data..." && \
    python ML_preprocess.py

# Define testing set
RUN echo "Defining testing set..." && \
    python test_set.py

# Select best subset of features
RUN echo "Selecting the best subset of features..." && \
    python Feature_Selection.py

# Train and apply a classification or regression model
RUN echo "Training and applying a classification or regression model..." && \
    python ML_classification.py  # or python ML_regression.py

# Assess results
RUN echo "Assessing the results..." && \
    python scripts_PostAnalysis.py

# Print a message after all steps are completed
RUN echo "All steps completed successfully."

# Set the default command to python3
CMD ["python3"]
