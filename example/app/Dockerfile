FROM python:3.5

# Install dependencies
RUN pip install pandas \
  numpy \
  sklearn \
  datetime

# Move to the app folder
RUN mkdir /app
WORKDIR /app

# Copy our python program for training and inference
COPY ./infer.py .


# Copy Bash scripts expected by the IT infrastructure of the EHR DREAM Challenge

COPY ./infer.sh .

# Add executable permission to Bash scripts
RUN chmod +x infer.sh
