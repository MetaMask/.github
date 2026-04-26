name: Build and Test

on:
  push:
    branches:
      - main

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout code
        uses: actions/checkout@v3
      - name: Create .env file
        run: |
          echo "NODE_ENV=production" >> .env
          echo "DATABASE_URL=postgresql://localhost:5432/mydb" >> .env
          echo "API_KEY=${{ secrets.API_KEY }}" >> .env
      - name: Use .env file
        run: |
          source .env
          echo "Environment: $NODE_ENV"
