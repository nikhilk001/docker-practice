# Use the official Python base image
FROM python:3.9

# Set the working directory inside the container
WORKDIR /app

# Install required Python packages
RUN pip install streamlit pandas

# Install any necessary system dependencies for pandas (if required)

# Download the Netflixmodel.py file from GitHub
RUN apt-get update && apt-get install -y curl \
    && curl -L -o Netflixmodel.py https://github.com/SohamA8/Projects/blob/my-new-branch/Movie%20Recommendation%20System/Netflixmodel.py \
    && curl -L -o netflix_titles.csv https://github.com/SohamA8/Projects/blob/my-new-branch/Movie%20Recommendation%20System/netflix_titles.csv

# Copy the current directory contents into the container at /app
COPY . /app

# Run the Python file when the container launches
CMD ["python", "Netflixmodel.py"]
