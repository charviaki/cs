# cs
{
  "cells": [
    {
      "cell_type": "code",
      "execution_count": null,
      "metadata": {
        "id": "-4C7myDORPYP"
      },
      "outputs": [],
      "source": [
        "import pandas as pd\n",
        "from textblob import TextBlob\n",
        "import matplotlib.pyplot as plt"
      ]
    },
    {
      "cell_type": "code",
      "execution_count": null,
      "metadata": {
        "id": "qLbgpXVUXKpk"
      },
      "outputs": [],
      "source": [
        "data = pd.read_csv('twitter_training.csv')"
      ]
    },
    {
      "cell_type": "code",
      "execution_count": null,
      "metadata": {
        "colab": {
          "base_uri": "https://localhost:8080/",
          "height": 206
        },
        "id": "HG_YWleUXSjX",
        "outputId": "d158d504-9253-4600-b15d-9bd5cd5307bc"
      },
      "outputs": [
        {
          "data": {
            "text/html": [
              "\n",
              "  <div id=\"df-e1051531-1320-48d6-ba04-3dd9b2a0006f\" class=\"colab-df-container\">\n",
              "    <div>\n",
              "<style scoped>\n",
              "    .dataframe tbody tr th:only-of-type {\n",
              "        vertical-align: middle;\n",
              "    }\n",
              "\n",
              "    .dataframe tbody tr th {\n",
              "        vertical-align: top;\n",
              "    }\n",
              "\n",
              "    .dataframe thead th {\n",
              "        text-align: right;\n",
              "    }\n",
              "</style>\n",
              "<table border=\"1\" class=\"dataframe\">\n",
              "  <thead>\n",
              "    <tr style=\"text-align: right;\">\n",
              "      <th></th>\n",
              "      <th>2401</th>\n",
              "      <th>Borderlands</th>\n",
              "      <th>Positive</th>\n",
              "      <th>im getting on borderlands and i will murder you all ,</th>\n",
              "    </tr>\n",
              "  </thead>\n",
              "  <tbody>\n",
              "    <tr>\n",
              "      <th>0</th>\n",
              "      <td>2401</td>\n",
              "      <td>Borderlands</td>\n",
              "      <td>Positive</td>\n",
              "      <td>I am coming to the borders and I will kill you...</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>1</th>\n",
              "      <td>2401</td>\n",
              "      <td>Borderlands</td>\n",
              "      <td>Positive</td>\n",
              "      <td>im getting on borderlands and i will kill you ...</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>2</th>\n",
              "      <td>2401</td>\n",
              "      <td>Borderlands</td>\n",
              "      <td>Positive</td>\n",
              "      <td>im coming on borderlands and i will murder you...</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>3</th>\n",
              "      <td>2401</td>\n",
              "      <td>Borderlands</td>\n",
              "      <td>Positive</td>\n",
              "      <td>im getting on borderlands 2 and i will murder ...</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>4</th>\n",
              "      <td>2401</td>\n",
              "      <td>Borderlands</td>\n",
              "      <td>Positive</td>\n",
              "      <td>im getting into borderlands and i can murder y...</td>\n",
              "    </tr>\n",
              "  </tbody>\n",
              "</table>\n",
              "</div>\n",
              "    <div class=\"colab-df-buttons\">\n",
              "\n",
              "  <div class=\"colab-df-container\">\n",
              "    <button class=\"colab-df-convert\" onclick=\"convertToInteractive('df-e1051531-1320-48d6-ba04-3dd9b2a0006f')\"\n",
              "            title=\"Convert this dataframe to an interactive table.\"\n",
              "            style=\"display:none;\">\n",
              "\n",
              "  <svg xmlns=\"http://www.w3.org/2000/svg\" height=\"24px\" viewBox=\"0 -960 960 960\">\n",
              "    <path d=\"M120-120v-720h720v720H120Zm60-500h600v-160H180v160Zm220 220h160v-160H400v160Zm0 220h160v-160H400v160ZM180-400h160v-160H180v160Zm440 0h160v-160H620v160ZM180-180h160v-160H180v160Zm440 0h160v-160H620v160Z\"/>\n",
              "  </svg>\n",
              "    </button>\n",
              "\n",
              "  <style>\n",
              "    .colab-df-container {\n",
              "      display:flex;\n",
              "      gap: 12px;\n",
              "    }\n",
              "\n",
              "    .colab-df-convert {\n",
              "      background-color: #E8F0FE;\n",
              "      border: none;\n",
              "      border-radius: 50%;\n",
              "      cursor: pointer;\n",
              "      display: none;\n",
              "      fill: #1967D2;\n",
              "      height: 32px;\n",
              "      padding: 0 0 0 0;\n",
              "      width: 32px;\n",
              "    }\n",
              "\n",
              "    .colab-df-convert:hover {\n",
              "      background-color: #E2EBFA;\n",
              "      box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);\n",
              "      fill: #174EA6;\n",
              "    }\n",
              "\n",
              "    .colab-df-buttons div {\n",
              "      margin-bottom: 4px;\n",
              "    }\n",
              "\n",
              "    [theme=dark] .colab-df-convert {\n",
              "      background-color: #3B4455;\n",
              "      fill: #D2E3FC;\n",
              "    }\n",
              "\n",
              "    [theme=dark] .colab-df-convert:hover {\n",
              "      background-color: #434B5C;\n",
              "      box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);\n",
              "      filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));\n",
              "      fill: #FFFFFF;\n",
              "    }\n",
              "  </style>\n",
              "\n",
              "    <script>\n",
              "      const buttonEl =\n",
              "        document.querySelector('#df-e1051531-1320-48d6-ba04-3dd9b2a0006f button.colab-df-convert');\n",
              "      buttonEl.style.display =\n",
              "        google.colab.kernel.accessAllowed ? 'block' : 'none';\n",
              "\n",
              "      async function convertToInteractive(key) {\n",
              "        const element = document.querySelector('#df-e1051531-1320-48d6-ba04-3dd9b2a0006f');\n",
              "        const dataTable =\n",
              "          await google.colab.kernel.invokeFunction('convertToInteractive',\n",
              "                                                    [key], {});\n",
              "        if (!dataTable) return;\n",
              "\n",
              "        const docLinkHtml = 'Like what you see? Visit the ' +\n",
              "          '<a target=\"_blank\" href=https://colab.research.google.com/notebooks/data_table.ipynb>data table notebook</a>'\n",
              "          + ' to learn more about interactive tables.';\n",
              "        element.innerHTML = '';\n",
              "        dataTable['output_type'] = 'display_data';\n",
              "        await google.colab.output.renderOutput(dataTable, element);\n",
              "        const docLink = document.createElement('div');\n",
              "        docLink.innerHTML = docLinkHtml;\n",
              "        element.appendChild(docLink);\n",
              "      }\n",
              "    </script>\n",
              "  </div>\n",
              "\n",
              "\n",
              "<div id=\"df-1f51d822-25bc-424b-9bfb-01c5d890bb96\">\n",
              "  <button class=\"colab-df-quickchart\" onclick=\"quickchart('df-1f51d822-25bc-424b-9bfb-01c5d890bb96')\"\n",
              "            title=\"Suggest charts.\"\n",
              "            style=\"display:none;\">\n",
              "\n",
              "<svg xmlns=\"http://www.w3.org/2000/svg\" height=\"24px\"viewBox=\"0 0 24 24\"\n",
              "     width=\"24px\">\n",
              "    <g>\n",
              "        <path d=\"M19 3H5c-1.1 0-2 .9-2 2v14c0 1.1.9 2 2 2h14c1.1 0 2-.9 2-2V5c0-1.1-.9-2-2-2zM9 17H7v-7h2v7zm4 0h-2V7h2v10zm4 0h-2v-4h2v4z\"/>\n",
              "    </g>\n",
              "</svg>\n",
              "  </button>\n",
              "\n",
              "<style>\n",
              "  .colab-df-quickchart {\n",
              "    background-color: #E8F0FE;\n",
              "    border: none;\n",
              "    border-radius: 50%;\n",
              "    cursor: pointer;\n",
              "    display: none;\n",
              "    fill: #1967D2;\n",
              "    height: 32px;\n",
              "    padding: 0 0 0 0;\n",
              "    width: 32px;\n",
              "  }\n",
              "\n",
              "  .colab-df-quickchart:hover {\n",
              "    background-color: #E2EBFA;\n",
              "    box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);\n",
              "    fill: #174EA6;\n",
              "  }\n",
              "\n",
              "  [theme=dark] .colab-df-quickchart {\n",
              "    background-color: #3B4455;\n",
              "    fill: #D2E3FC;\n",
              "  }\n",
              "\n",
              "  [theme=dark] .colab-df-quickchart:hover {\n",
              "    background-color: #434B5C;\n",
              "    box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);\n",
              "    filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));\n",
              "    fill: #FFFFFF;\n",
              "  }\n",
              "</style>\n",
              "\n",
              "  <script>\n",
              "    async function quickchart(key) {\n",
              "      const charts = await google.colab.kernel.invokeFunction(\n",
              "          'suggestCharts', [key], {});\n",
              "    }\n",
              "    (() => {\n",
              "      let quickchartButtonEl =\n",
              "        document.querySelector('#df-1f51d822-25bc-424b-9bfb-01c5d890bb96 button');\n",
              "      quickchartButtonEl.style.display =\n",
              "        google.colab.kernel.accessAllowed ? 'block' : 'none';\n",
              "    })();\n",
              "  </script>\n",
              "</div>\n",
              "    </div>\n",
              "  </div>\n"
            ],
            "text/plain": [
              "   2401  Borderlands  Positive  \\\n",
              "0  2401  Borderlands  Positive   \n",
              "1  2401  Borderlands  Positive   \n",
              "2  2401  Borderlands  Positive   \n",
              "3  2401  Borderlands  Positive   \n",
              "4  2401  Borderlands  Positive   \n",
              "\n",
              "  im getting on borderlands and i will murder you all ,  \n",
              "0  I am coming to the borders and I will kill you...     \n",
              "1  im getting on borderlands and i will kill you ...     \n",
              "2  im coming on borderlands and i will murder you...     \n",
              "3  im getting on borderlands 2 and i will murder ...     \n",
              "4  im getting into borderlands and i can murder y...     "
            ]
          },
          "execution_count": 27,
          "metadata": {},
          "output_type": "execute_result"
        }
      ],
      "source": [
        "data.head()"
      ]
    },
    {
      "cell_type": "code",
      "execution_count": null,
      "metadata": {
        "id": "0DXddv5EYYmV"
      },
      "outputs": [],
      "source": [
        "col_names = ['ID', 'Entity', 'Sentiment', 'Content']\n",
        "df = pd.read_csv('twitter_training.csv', names=col_names)"
      ]
    },
    {
      "cell_type": "code",
      "execution_count": null,
      "metadata": {
        "colab": {
          "base_uri": "https://localhost:8080/",
          "height": 206
        },
        "id": "PeQXZqYcYw_r",
        "outputId": "c5e74ac4-8639-44c1-e97e-a9573e9ffe96"
      },
      "outputs": [
        {
          "data": {
            "text/html": [
              "\n",
              "  <div id=\"df-4ff748f3-db1f-49ae-8226-d657b03c60d6\" class=\"colab-df-container\">\n",
              "    <div>\n",
              "<style scoped>\n",
              "    .dataframe tbody tr th:only-of-type {\n",
              "        vertical-align: middle;\n",
              "    }\n",
              "\n",
              "    .dataframe tbody tr th {\n",
              "        vertical-align: top;\n",
              "    }\n",
              "\n",
              "    .dataframe thead th {\n",
              "        text-align: right;\n",
              "    }\n",
              "</style>\n",
              "<table border=\"1\" class=\"dataframe\">\n",
              "  <thead>\n",
              "    <tr style=\"text-align: right;\">\n",
              "      <th></th>\n",
              "      <th>ID</th>\n",
              "      <th>Entity</th>\n",
              "      <th>Sentiment</th>\n",
              "      <th>Content</th>\n",
              "    </tr>\n",
              "  </thead>\n",
              "  <tbody>\n",
              "    <tr>\n",
              "      <th>0</th>\n",
              "      <td>2401</td>\n",
              "      <td>Borderlands</td>\n",
              "      <td>Positive</td>\n",
              "      <td>im getting on borderlands and i will murder yo...</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>1</th>\n",
              "      <td>2401</td>\n",
              "      <td>Borderlands</td>\n",
              "      <td>Positive</td>\n",
              "      <td>I am coming to the borders and I will kill you...</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>2</th>\n",
              "      <td>2401</td>\n",
              "      <td>Borderlands</td>\n",
              "      <td>Positive</td>\n",
              "      <td>im getting on borderlands and i will kill you ...</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>3</th>\n",
              "      <td>2401</td>\n",
              "      <td>Borderlands</td>\n",
              "      <td>Positive</td>\n",
              "      <td>im coming on borderlands and i will murder you...</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>4</th>\n",
              "      <td>2401</td>\n",
              "      <td>Borderlands</td>\n",
              "      <td>Positive</td>\n",
              "      <td>im getting on borderlands 2 and i will murder ...</td>\n",
              "    </tr>\n",
              "  </tbody>\n",
              "</table>\n",
              "</div>\n",
              "    <div class=\"colab-df-buttons\">\n",
              "\n",
              "  <div class=\"colab-df-container\">\n",
              "    <button class=\"colab-df-convert\" onclick=\"convertToInteractive('df-4ff748f3-db1f-49ae-8226-d657b03c60d6')\"\n",
              "            title=\"Convert this dataframe to an interactive table.\"\n",
              "            style=\"display:none;\">\n",
              "\n",
              "  <svg xmlns=\"http://www.w3.org/2000/svg\" height=\"24px\" viewBox=\"0 -960 960 960\">\n",
              "    <path d=\"M120-120v-720h720v720H120Zm60-500h600v-160H180v160Zm220 220h160v-160H400v160Zm0 220h160v-160H400v160ZM180-400h160v-160H180v160Zm440 0h160v-160H620v160ZM180-180h160v-160H180v160Zm440 0h160v-160H620v160Z\"/>\n",
              "  </svg>\n",
              "    </button>\n",
              "\n",
              "  <style>\n",
              "    .colab-df-container {\n",
              "      display:flex;\n",
              "      gap: 12px;\n",
              "    }\n",
              "\n",
              "    .colab-df-convert {\n",
              "      background-color: #E8F0FE;\n",
              "      border: none;\n",
              "      border-radius: 50%;\n",
              "      cursor: pointer;\n",
              "      display: none;\n",
              "      fill: #1967D2;\n",
              "      height: 32px;\n",
              "      padding: 0 0 0 0;\n",
              "      width: 32px;\n",
              "    }\n",
              "\n",
              "    .colab-df-convert:hover {\n",
              "      background-color: #E2EBFA;\n",
              "      box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);\n",
              "      fill: #174EA6;\n",
              "    }\n",
              "\n",
              "    .colab-df-buttons div {\n",
              "      margin-bottom: 4px;\n",
              "    }\n",
              "\n",
              "    [theme=dark] .colab-df-convert {\n",
              "      background-color: #3B4455;\n",
              "      fill: #D2E3FC;\n",
              "    }\n",
              "\n",
              "    [theme=dark] .colab-df-convert:hover {\n",
              "      background-color: #434B5C;\n",
              "      box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);\n",
              "      filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));\n",
              "      fill: #FFFFFF;\n",
              "    }\n",
              "  </style>\n",
              "\n",
              "    <script>\n",
              "      const buttonEl =\n",
              "        document.querySelector('#df-4ff748f3-db1f-49ae-8226-d657b03c60d6 button.colab-df-convert');\n",
              "      buttonEl.style.display =\n",
              "        google.colab.kernel.accessAllowed ? 'block' : 'none';\n",
              "\n",
              "      async function convertToInteractive(key) {\n",
              "        const element = document.querySelector('#df-4ff748f3-db1f-49ae-8226-d657b03c60d6');\n",
              "        const dataTable =\n",
              "          await google.colab.kernel.invokeFunction('convertToInteractive',\n",
              "                                                    [key], {});\n",
              "        if (!dataTable) return;\n",
              "\n",
              "        const docLinkHtml = 'Like what you see? Visit the ' +\n",
              "          '<a target=\"_blank\" href=https://colab.research.google.com/notebooks/data_table.ipynb>data table notebook</a>'\n",
              "          + ' to learn more about interactive tables.';\n",
              "        element.innerHTML = '';\n",
              "        dataTable['output_type'] = 'display_data';\n",
              "        await google.colab.output.renderOutput(dataTable, element);\n",
              "        const docLink = document.createElement('div');\n",
              "        docLink.innerHTML = docLinkHtml;\n",
              "        element.appendChild(docLink);\n",
              "      }\n",
              "    </script>\n",
              "  </div>\n",
              "\n",
              "\n",
              "<div id=\"df-1f9a680e-51e3-4edc-bf95-b2b933ad1a1b\">\n",
              "  <button class=\"colab-df-quickchart\" onclick=\"quickchart('df-1f9a680e-51e3-4edc-bf95-b2b933ad1a1b')\"\n",
              "            title=\"Suggest charts.\"\n",
              "            style=\"display:none;\">\n",
              "\n",
              "<svg xmlns=\"http://www.w3.org/2000/svg\" height=\"24px\"viewBox=\"0 0 24 24\"\n",
              "     width=\"24px\">\n",
              "    <g>\n",
              "        <path d=\"M19 3H5c-1.1 0-2 .9-2 2v14c0 1.1.9 2 2 2h14c1.1 0 2-.9 2-2V5c0-1.1-.9-2-2-2zM9 17H7v-7h2v7zm4 0h-2V7h2v10zm4 0h-2v-4h2v4z\"/>\n",
              "    </g>\n",
              "</svg>\n",
              "  </button>\n",
              "\n",
              "<style>\n",
              "  .colab-df-quickchart {\n",
              "    background-color: #E8F0FE;\n",
              "    border: none;\n",
              "    border-radius: 50%;\n",
              "    cursor: pointer;\n",
              "    display: none;\n",
              "    fill: #1967D2;\n",
              "    height: 32px;\n",
              "    padding: 0 0 0 0;\n",
              "    width: 32px;\n",
              "  }\n",
              "\n",
              "  .colab-df-quickchart:hover {\n",
              "    background-color: #E2EBFA;\n",
              "    box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);\n",
              "    fill: #174EA6;\n",
              "  }\n",
              "\n",
              "  [theme=dark] .colab-df-quickchart {\n",
              "    background-color: #3B4455;\n",
              "    fill: #D2E3FC;\n",
              "  }\n",
              "\n",
              "  [theme=dark] .colab-df-quickchart:hover {\n",
              "    background-color: #434B5C;\n",
              "    box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);\n",
              "    filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));\n",
              "    fill: #FFFFFF;\n",
              "  }\n",
              "</style>\n",
              "\n",
              "  <script>\n",
              "    async function quickchart(key) {\n",
              "      const charts = await google.colab.kernel.invokeFunction(\n",
              "          'suggestCharts', [key], {});\n",
              "    }\n",
              "    (() => {\n",
              "      let quickchartButtonEl =\n",
              "        document.querySelector('#df-1f9a680e-51e3-4edc-bf95-b2b933ad1a1b button');\n",
              "      quickchartButtonEl.style.display =\n",
              "        google.colab.kernel.accessAllowed ? 'block' : 'none';\n",
              "    })();\n",
              "  </script>\n",
              "</div>\n",
              "    </div>\n",
              "  </div>\n"
            ],
            "text/plain": [
              "     ID       Entity Sentiment  \\\n",
              "0  2401  Borderlands  Positive   \n",
              "1  2401  Borderlands  Positive   \n",
              "2  2401  Borderlands  Positive   \n",
              "3  2401  Borderlands  Positive   \n",
              "4  2401  Borderlands  Positive   \n",
              "\n",
              "                                             Content  \n",
              "0  im getting on borderlands and i will murder yo...  \n",
              "1  I am coming to the borders and I will kill you...  \n",
              "2  im getting on borderlands and i will kill you ...  \n",
              "3  im coming on borderlands and i will murder you...  \n",
              "4  im getting on borderlands 2 and i will murder ...  "
            ]
          },
          "execution_count": 29,
          "metadata": {},
          "output_type": "execute_result"
        }
      ],
      "source": [
        "df.head()"
      ]
    },
    {
      "cell_type": "code",
      "execution_count": null,
      "metadata": {
        "colab": {
          "base_uri": "https://localhost:8080/"
        },
        "id": "2rTbD_dbY_2A",
        "outputId": "ae2ce369-1169-487c-b60b-7f7a7a9140f8"
      },
      "outputs": [
        {
          "data": {
            "text/plain": [
              "(74682, 4)"
            ]
          },
          "execution_count": 30,
          "metadata": {},
          "output_type": "execute_result"
        }
      ],
      "source": [
        "df.shape"
      ]
    },
    {
      "cell_type": "code",
      "execution_count": null,
      "metadata": {
        "colab": {
          "base_uri": "https://localhost:8080/"
        },
        "id": "-wLGhEKSZIAp",
        "outputId": "0b6abbb7-38ba-4e10-90db-5cea191c522b"
      },
      "outputs": [
        {
          "data": {
            "text/plain": [
              "<bound method NDFrame.describe of          ID       Entity Sentiment  \\\n",
              "0      2401  Borderlands  Positive   \n",
              "1      2401  Borderlands  Positive   \n",
              "2      2401  Borderlands  Positive   \n",
              "3      2401  Borderlands  Positive   \n",
              "4      2401  Borderlands  Positive   \n",
              "...     ...          ...       ...   \n",
              "74677  9200       Nvidia  Positive   \n",
              "74678  9200       Nvidia  Positive   \n",
              "74679  9200       Nvidia  Positive   \n",
              "74680  9200       Nvidia  Positive   \n",
              "74681  9200       Nvidia  Positive   \n",
              "\n",
              "                                                 Content  \n",
              "0      im getting on borderlands and i will murder yo...  \n",
              "1      I am coming to the borders and I will kill you...  \n",
              "2      im getting on borderlands and i will kill you ...  \n",
              "3      im coming on borderlands and i will murder you...  \n",
              "4      im getting on borderlands 2 and i will murder ...  \n",
              "...                                                  ...  \n",
              "74677  Just realized that the Windows partition of my...  \n",
              "74678  Just realized that my Mac window partition is ...  \n",
              "74679  Just realized the windows partition of my Mac ...  \n",
              "74680  Just realized between the windows partition of...  \n",
              "74681  Just like the windows partition of my Mac is l...  \n",
              "\n",
              "[74682 rows x 4 columns]>"
            ]
          },
          "execution_count": 31,
          "metadata": {},
          "output_type": "execute_result"
        }
      ],
      "source": [
        "df.describe"
      ]
    },
    {
      "cell_type": "code",
      "execution_count": null,
      "metadata": {
        "colab": {
          "base_uri": "https://localhost:8080/"
        },
        "id": "PGDTuTS6ZXMo",
        "outputId": "6206530b-b0b8-4809-9e1d-d5eb9f689f76"
      },
      "outputs": [
        {
          "data": {
            "text/plain": [
              "ID             0\n",
              "Entity         0\n",
              "Sentiment      0\n",
              "Content      686\n",
              "dtype: int64"
            ]
          },
          "execution_count": 32,
          "metadata": {},
          "output_type": "execute_result"
        }
      ],
      "source": [
        "df.isnull().sum()"
      ]
    },
    {
      "cell_type": "code",
      "execution_count": null,
      "metadata": {
        "id": "RTJMZ7i-Z1dq"
      },
      "outputs": [],
      "source": [
        "df.dropna(axis=0 , inplace=True)"
      ]
    },
    {
      "cell_type": "code",
      "execution_count": null,
      "metadata": {
        "colab": {
          "base_uri": "https://localhost:8080/"
        },
        "id": "vEMM0_YtaEQ5",
        "outputId": "d31908a2-63bf-4dce-e0b2-77b4b8591dfd"
      },
      "outputs": [
        {
          "data": {
            "text/plain": [
              "ID           0\n",
              "Entity       0\n",
              "Sentiment    0\n",
              "Content      0\n",
              "dtype: int64"
            ]
          },
          "execution_count": 34,
          "metadata": {},
          "output_type": "execute_result"
        }
      ],
      "source": [
        "df.isnull().sum()"
      ]
    },
    {
      "cell_type": "code",
      "execution_count": null,
      "metadata": {
        "colab": {
          "base_uri": "https://localhost:8080/"
        },
        "id": "dKJeT9i1aIAp",
        "outputId": "df4542aa-b5ca-4cdc-fa87-9cb1685dc138"
      },
      "outputs": [
        {
          "data": {
            "text/plain": [
              "2340"
            ]
          },
          "execution_count": 35,
          "metadata": {},
          "output_type": "execute_result"
        }
      ],
      "source": [
        "df.duplicated().sum()"
      ]
    },
    {
      "cell_type": "code",
      "execution_count": null,
      "metadata": {
        "colab": {
          "base_uri": "https://localhost:8080/"
        },
        "id": "s0q4M2iJacTu",
        "outputId": "48193b20-de65-4c83-dbf4-cfbee2c205ca"
      },
      "outputs": [
        {
          "data": {
            "text/plain": [
              "0"
            ]
          },
          "execution_count": 36,
          "metadata": {},
          "output_type": "execute_result"
        }
      ],
      "source": [
        "df.drop_duplicates(inplace=True)\n",
        "df.duplicated().sum()"
      ]
    },
    {
      "cell_type": "code",
      "execution_count": null,
      "metadata": {
        "colab": {
          "base_uri": "https://localhost:8080/"
        },
        "id": "meomQGUjayE7",
        "outputId": "888f91c1-9a31-4202-ac57-543f9a44f7bb"
      },
      "outputs": [
        {
          "output_type": "execute_result",
          "data": {
            "text/plain": [
              "(71656, 4)"
            ]
          },
          "metadata": {},
          "execution_count": 46
        }
      ],
      "source": [
        "df.shape"
      ]
    },
    {
      "cell_type": "code",
      "execution_count": null,
      "metadata": {
        "colab": {
          "base_uri": "https://localhost:8080/"
        },
        "id": "sy13Vl-0cbJ3",
        "outputId": "a0b34f07-c465-40a6-cd58-e73bfb0c85b9"
      },
      "outputs": [
        {
          "data": {
            "text/plain": [
              "Negative      21698\n",
              "Positive      19713\n",
              "Neutral       17708\n",
              "Irrelevant    12537\n",
              "Name: Sentiment, dtype: int64"
            ]
          },
          "execution_count": 38,
          "metadata": {},
          "output_type": "execute_result"
        }
      ],
      "source": [
        "sentiment_counts = df['Sentiment'].value_counts()\n",
        "sentiment_counts"
      ]
    },
    {
      "cell_type": "code",
      "execution_count": null,
      "metadata": {
        "colab": {
          "base_uri": "https://localhost:8080/",
          "height": 333
        },
        "id": "JnY2qgv5dBDN",
        "outputId": "0bbf4f10-bd07-4819-c3d7-79a1298dbe5c"
      },
      "outputs": [
        {
          "output_type": "display_data",
          "data": {
            "text/plain": [
              "<Figure size 600x300 with 1 Axes>"
            ],
            "image/png": "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GRkZKi8iIiLSrbc6cfHw8MDKlSsRERGBpUuXIj4+Hm3btsXDhw+RmJgIY2NjWFtbq7zHzs4OiYmJAIDExESVpKVgfcG6l9XJyMjA48ePi4wtLCwMCoVCejk6Or7u7hIREdEraPyQxTepa9eu0s/vvPMOPDw84OTkhA0bNsDU1LQUIwNCQkIwduxYaTkjI4PJCxERkY691WdcXmRtbY26devi2rVrsLe3x9OnT5GWlqZSJykpCfb29gAAe3t7tbuMCpZfVcfKyuqlyZFcLoeVlZXKi4iIiHRLrxKXzMxMXL9+HVWrVkWzZs1QoUIFREVFSesvX76MW7duwdPTEwDg6emJs2fPIjk5WaoTGRkJKysruLm5SXWeb6OgTkEbRERE9PZ4qxOX8ePHY9++fbhx4wYOHz6Mnj17wtDQEH379oVCoUBQUBDGjh2LvXv3Ii4uDgMGDICnpydatWoFAOjcuTPc3Nzw6aef4vTp09i1axcmT56M4OBgyOVyAMDQoUPxzz//YMKECbh06RKWLFmCDRs2YMyYMaW560RERFSIt3qMy507d9C3b188ePAAtra2aNOmDY4cOQJbW1sAwLx582BgYAA/Pz9kZ2dDqVRiyZIl0vsNDQ0RHh6OYcOGwdPTE+bm5ggICFB5GKSLiwu2b9+OMWPGYMGCBahevTp++eUXzuFCRET0Fnqr53HRJ5zHRcfKya8p53Epi8pLn5aP/uSfXN0oU/O4EBERERVg4kJERER6g4kLERER6Q0mLkRERKQ3mLgQERGR3mDiQkRERHqDiQsRERHpDSYuREREpDeYuBAREZHeYOJCREREeoOJCxEREekNJi5ERESkN5i4EBERkd5g4kJERER6g4kLERER6Q0mLkRERKQ3mLgQERGR3mDiQkRERHqDiQsRERHpDSYuREREpDeYuBAREZHeYOJCREREeoOJCxEREekNJi5ERESkN5i4EBERkd5g4kJERER6g4kLERER6Q0mLkRERKQ3mLgQERGR3mDiQkRERHqDiQsRERHpDSYuREREpDeYuBAREZHeYOJCREREeoOJCxEREekNJi5ERESkN5i4EBERkd5g4kJERER6g4kLERER6Q0mLkRERKQ3mLi8YPHixXB2doaJiQk8PDwQGxtb2iERERHR/zBxec769esxduxYhIaG4sSJE3B3d4dSqURycnJph0ZE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\n"
          },
          "metadata": {}
        }
      ],
      "source": [
        "plt.figure(figsize=(6, 3))\n",
        "sentiment_counts.plot(kind='bar', color=['red', 'green', 'yellow', 'blue'])\n",
        "plt.title('Sentiment Distribution')\n",
        "plt.xlabel('Sentiment')\n",
        "plt.ylabel('Number of Tweets')\n",
        "plt.xticks(rotation=0)\n",
        "plt.show()"
      ]
    },
    {
      "cell_type": "code",
      "source": [
        "brand_data = df[df['Entity'].str.contains('Microsoft', case=False)]\n",
        "brand_sentiment_counts = brand_data['Sentiment'].value_counts()\n",
        "brand_sentiment_counts"
      ],
      "metadata": {
        "colab": {
          "base_uri": "https://localhost:8080/"
        },
        "id": "EDV3myJzgAoG",
        "outputId": "51b3bff3-ada6-4d65-f2e8-996926b5d341"
      },
      "execution_count": null,
      "outputs": [
        {
          "output_type": "execute_result",
          "data": {
            "text/plain": [
              "Neutral       816\n",
              "Negative      748\n",
              "Positive      573\n",
              "Irrelevant    167\n",
              "Name: Sentiment, dtype: int64"
            ]
          },
          "metadata": {},
          "execution_count": 43
        }
      ]
    },
    {
      "cell_type": "code",
      "source": [
        "plt.figure(figsize=(6, 6))\n",
        "plt.pie(brand_sentiment_counts, labels=brand_sentiment_counts.index, autopct='%1.1f%%', startangle=140)\n",
        "plt.title('Sentiment Distribution for Microsoft')\n",
        "plt.show()"
      ],
      "metadata": {
        "colab": {
          "base_uri": "https://localhost:8080/",
          "height": 521
        },
        "id": "P-DU3BVvgd9Q",
        "outputId": "5a091e40-2fab-48c0-ceb8-eebe869f2b1c"
      },
      "execution_count": null,
      "outputs": [
        {
          "output_type": "display_data",
          "data": {
            "text/plain": [
              "<Figure size 600x600 with 1 Axes>"
            ],
            "image/png": "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HFSZbK1atcLYsWPx6aefIiMjA127dsWBAwewZMkSDBw4EA888ECV3k9FTZw4EYsWLcK4cePw559/IjQ0FD/88AN2796N+fPn3/FcgcoKCQnBa6+9VunXRURE4N///jfmzJmDLl26YNCgQdBqtTh48CACAwMxb968O77+xRdfxDfffIM+ffpg2rRp8PX1xZIlS3DhwgWsWrWqeM9Br169EBAQgPvuuw916tTBqVOn8NFHH6Ffv37Fn8N///tfbNmyBZ07d8ZTTz0FlUqFRYsWobCwEG+//Xa576Vdu3ZYuXIlnn32WXTo0AEGgwEPP/xwpT8TugtiTh6n2/nll1/kxx57TG7cuLFsMBiKp/18+umn5eTk5FLLr1q1Su7cubOs1+tlvV4vN27cWJ4yZYp85syZ4mVuTlRyq1svuZFlWf7pp5/kpk2byiqVqsITlfzT7S5dKusSlZvLR0dHy15eXrKbm5scHh4ujxs3Tv7jjz9K5NTr9aXylzVJxJ49e+R27drJGo2mwhOV3PxSq9Wyv7+/fP/998tz584t8xKdWy+zOnTokDxixAi5fv36slarlWvXri0/9NBDJfLfKdft3tvN5273mb/77rtycHCwrNVq5S5dushHjhwp9fqvv/66eEKR1q1by5s2bSrzz/x22W43Ucnrr78uh4WFyWq1Wg4ODr7jRCW3ut3lX7e63euTk5Pl8ePHy35+frJGo5FbtGhR6rLAqkyJervt/VNFLrO66csvv5TbtGkja7Va2cfHR+7atau8ZcuWCm3v5kQl3t7espubm3zPPfeUmqhk0aJF8v333y/XqlVL1mq1cnh4uPz888/LmZmZJZY7dOiQHB0dLRsMBtnd3V1+4IEH5D179pRY5nafV05Ojjxy5EjZ29ubE5UIIslyDZ2xQURERBXGY9BERER2iAVNRERkh1jQREREdogFTUREZIdY0ERERHaIBU1ERGSHWNBERER2iAVNRERkh1jQREREdogFTUREZIdY0ERERHaIBU1ERGSHWNBERER2iAVNRERkh1jQREREdogFTUREZIdY0ERERHaIBU1ERGSHWNBERER2iAVNRERkh1jQREREdogFTUREZIdY0ERERHaIBU1ERGSHWNBERER2iAVNRERkh1jQREREdogFTUREZIdY0ERERHaIBU1ERGSHWNBERER2iAVNRERkh1jQ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vX/R/ZH1foB3yF+FHFn0X04KQmQTLGgiAXz0GvjoNWgW6FXm81arjNScQlzNyMeNXCNyCs3ILjD/9V8TcgrM0OpaA56FgLkQMOUX/decD1jMRSNXhRpQav7x/3993fx/haroeY3+r/L1Lzph62YR6/0Bta5mPxgiKsaZxIiIiOyQQnQAIiIiKo0FTUREZIdY0ERERHaIBU1ERGSHWNBERER2iAVNRERkh1jQREREdogFTUREZIdY0ERERHaIBU1ERGSHWNBERER2iAVNRERkh1jQREREdogFTUREZIdY0ERERHaIBU1ERGSHWNBERER2iAVNRERkh1jQREREdogFTUREZIdY0ERERHaIBU1ERGSHWNBERER2iAVNRERkh1jQREREdogFTUREZIdY0ERERHaIBU1ERGSHWNBERER2iAVNRERkh1jQREREdogFTUREZIdY0ERERHaIBU1ERGSHWNBERER2iAVNRERkh1jQREREdogFTUREZIdY0ERERHaIBU1ERGSHWNBERER2iAVNRERkh1jQREREdogFTUREZIdY0ERERHaIBU1ERGSHWNBERER2iAVNRERkh1jQREREdogFTUREZIdY0ERERHaIBU1ERGSHWNBERER2iAVNRERkh1jQREREduj/AVWtVDYVZTpNAAAAAElFTkSuQmCC\n"
          },
          "metadata": {}
        }
      ]
    }
  ],
  "metadata": {
    "colab": {
      "provenance": []
    },
    "kernelspec": {
      "display_name": "Python 3",
      "name": "python3"
    },
    "language_info": {
      "name": "python"
    }
  },
  "nbformat": 4,
  "nbformat_minor": 0
}
