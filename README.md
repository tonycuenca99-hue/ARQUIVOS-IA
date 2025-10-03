# ARQUIVOS-IA
{
  "cells": [
    {
      "cell_type": "markdown",
      "metadata": {
        "id": "view-in-github",
        "colab_type": "text"
      },
      "source": [
        "<a href=\"https://colab.research.google.com/github/tonycuenca99-hue/ARQUIVOS-IA/blob/main/AULA%203\" target=\"_parent\"><img src=\"https://colab.research.google.com/assets/colab-badge.svg\" alt=\"Open In Colab\"/></a>"
      ]
    },
    {
      "cell_type": "code",
      "execution_count": null,
      "metadata": {
        "id": "ykAow5NxhcXj"
      },
      "outputs": [],
      "source": [
        "import pandas as pd\n",
        "import numpy as np\n",
        "import matplotlib.pyplot as plt\n"
      ]
    },
    {
      "cell_type": "code",
      "execution_count": null,
      "metadata": {
        "id": "5G1K4Lwnidvu"
      },
      "outputs": [],
      "source": [
        "from google.colab import files"
      ]
    },
    {
      "cell_type": "code",
      "execution_count": null,
      "metadata": {
        "colab": {
          "base_uri": "https://localhost:8080/"
        },
        "id": "39sGBoAYls9e",
        "outputId": "5597def8-bcfa-4fa2-bbda-47e1caf5a2e2"
      },
      "outputs": [
        {
          "output_type": "stream",
          "name": "stdout",
          "text": [
            "Mounted at /content/drive\n"
          ]
        }
      ],
      "source": [
        "from google.colab import drive\n",
        "drive.mount('/content/drive')"
      ]
    },
    {
      "cell_type": "code",
      "execution_count": null,
      "metadata": {
        "colab": {
          "base_uri": "https://localhost:8080/",
          "height": 73
        },
        "id": "tlZmdckymAKg",
        "outputId": "40c64699-d485-4e8d-c55e-22f0b3751ead"
      },
      "outputs": [
        {
          "output_type": "display_data",
          "data": {
            "text/plain": [
              "<IPython.core.display.HTML object>"
            ],
            "text/html": [
              "\n",
              "     <input type=\"file\" id=\"files-80eb367a-e5f7-46df-8a0f-03988ba2c170\" name=\"files[]\" multiple disabled\n",
              "        style=\"border:none\" />\n",
              "     <output id=\"result-80eb367a-e5f7-46df-8a0f-03988ba2c170\">\n",
              "      Upload widget is only available when the cell has been executed in the\n",
              "      current browser session. Please rerun this cell to enable.\n",
              "      </output>\n",
              "      <script>// Copyright 2017 Google LLC\n",
              "//\n",
              "// Licensed under the Apache License, Version 2.0 (the \"License\");\n",
              "// you may not use this file except in compliance with the License.\n",
              "// You may obtain a copy of the License at\n",
              "//\n",
              "//      http://www.apache.org/licenses/LICENSE-2.0\n",
              "//\n",
              "// Unless required by applicable law or agreed to in writing, software\n",
              "// distributed under the License is distributed on an \"AS IS\" BASIS,\n",
              "// WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.\n",
              "// See the License for the specific language governing permissions and\n",
              "// limitations under the License.\n",
              "\n",
              "/**\n",
              " * @fileoverview Helpers for google.colab Python module.\n",
              " */\n",
              "(function(scope) {\n",
              "function span(text, styleAttributes = {}) {\n",
              "  const element = document.createElement('span');\n",
              "  element.textContent = text;\n",
              "  for (const key of Object.keys(styleAttributes)) {\n",
              "    element.style[key] = styleAttributes[key];\n",
              "  }\n",
              "  return element;\n",
              "}\n",
              "\n",
              "// Max number of bytes which will be uploaded at a time.\n",
              "const MAX_PAYLOAD_SIZE = 100 * 1024;\n",
              "\n",
              "function _uploadFiles(inputId, outputId) {\n",
              "  const steps = uploadFilesStep(inputId, outputId);\n",
              "  const outputElement = document.getElementById(outputId);\n",
              "  // Cache steps on the outputElement to make it available for the next call\n",
              "  // to uploadFilesContinue from Python.\n",
              "  outputElement.steps = steps;\n",
              "\n",
              "  return _uploadFilesContinue(outputId);\n",
              "}\n",
              "\n",
              "// This is roughly an async generator (not supported in the browser yet),\n",
              "// where there are multiple asynchronous steps and the Python side is going\n",
              "// to poll for completion of each step.\n",
              "// This uses a Promise to block the python side on completion of each step,\n",
              "// then passes the result of the previous step as the input to the next step.\n",
              "function _uploadFilesContinue(outputId) {\n",
              "  const outputElement = document.getElementById(outputId);\n",
              "  const steps = outputElement.steps;\n",
              "\n",
              "  const next = steps.next(outputElement.lastPromiseValue);\n",
              "  return Promise.resolve(next.value.promise).then((value) => {\n",
              "    // Cache the last promise value to make it available to the next\n",
              "    // step of the generator.\n",
              "    outputElement.lastPromiseValue = value;\n",
              "    return next.value.response;\n",
              "  });\n",
              "}\n",
              "\n",
              "/**\n",
              " * Generator function which is called between each async step of the upload\n",
              " * process.\n",
              " * @param {string} inputId Element ID of the input file picker element.\n",
              " * @param {string} outputId Element ID of the output display.\n",
              " * @return {!Iterable<!Object>} Iterable of next steps.\n",
              " */\n",
              "function* uploadFilesStep(inputId, outputId) {\n",
              "  const inputElement = document.getElementById(inputId);\n",
              "  inputElement.disabled = false;\n",
              "\n",
              "  const outputElement = document.getElementById(outputId);\n",
              "  outputElement.innerHTML = '';\n",
              "\n",
              "  const pickedPromise = new Promise((resolve) => {\n",
              "    inputElement.addEventListener('change', (e) => {\n",
              "      resolve(e.target.files);\n",
              "    });\n",
              "  });\n",
              "\n",
              "  const cancel = document.createElement('button');\n",
              "  inputElement.parentElement.appendChild(cancel);\n",
              "  cancel.textContent = 'Cancel upload';\n",
              "  const cancelPromise = new Promise((resolve) => {\n",
              "    cancel.onclick = () => {\n",
              "      resolve(null);\n",
              "    };\n",
              "  });\n",
              "\n",
              "  // Wait for the user to pick the files.\n",
              "  const files = yield {\n",
              "    promise: Promise.race([pickedPromise, cancelPromise]),\n",
              "    response: {\n",
              "      action: 'starting',\n",
              "    }\n",
              "  };\n",
              "\n",
              "  cancel.remove();\n",
              "\n",
              "  // Disable the input element since further picks are not allowed.\n",
              "  inputElement.disabled = true;\n",
              "\n",
              "  if (!files) {\n",
              "    return {\n",
              "      response: {\n",
              "        action: 'complete',\n",
              "      }\n",
              "    };\n",
              "  }\n",
              "\n",
              "  for (const file of files) {\n",
              "    const li = document.createElement('li');\n",
              "    li.append(span(file.name, {fontWeight: 'bold'}));\n",
              "    li.append(span(\n",
              "        `(${file.type || 'n/a'}) - ${file.size} bytes, ` +\n",
              "        `last modified: ${\n",
              "            file.lastModifiedDate ? file.lastModifiedDate.toLocaleDateString() :\n",
              "                                    'n/a'} - `));\n",
              "    const percent = span('0% done');\n",
              "    li.appendChild(percent);\n",
              "\n",
              "    outputElement.appendChild(li);\n",
              "\n",
              "    const fileDataPromise = new Promise((resolve) => {\n",
              "      const reader = new FileReader();\n",
              "      reader.onload = (e) => {\n",
              "        resolve(e.target.result);\n",
              "      };\n",
              "      reader.readAsArrayBuffer(file);\n",
              "    });\n",
              "    // Wait for the data to be ready.\n",
              "    let fileData = yield {\n",
              "      promise: fileDataPromise,\n",
              "      response: {\n",
              "        action: 'continue',\n",
              "      }\n",
              "    };\n",
              "\n",
              "    // Use a chunked sending to avoid message size limits. See b/62115660.\n",
              "    let position = 0;\n",
              "    do {\n",
              "      const length = Math.min(fileData.byteLength - position, MAX_PAYLOAD_SIZE);\n",
              "      const chunk = new Uint8Array(fileData, position, length);\n",
              "      position += length;\n",
              "\n",
              "      const base64 = btoa(String.fromCharCode.apply(null, chunk));\n",
              "      yield {\n",
              "        response: {\n",
              "          action: 'append',\n",
              "          file: file.name,\n",
              "          data: base64,\n",
              "        },\n",
              "      };\n",
              "\n",
              "      let percentDone = fileData.byteLength === 0 ?\n",
              "          100 :\n",
              "          Math.round((position / fileData.byteLength) * 100);\n",
              "      percent.textContent = `${percentDone}% done`;\n",
              "\n",
              "    } while (position < fileData.byteLength);\n",
              "  }\n",
              "\n",
              "  // All done.\n",
              "  yield {\n",
              "    response: {\n",
              "      action: 'complete',\n",
              "    }\n",
              "  };\n",
              "}\n",
              "\n",
              "scope.google = scope.google || {};\n",
              "scope.google.colab = scope.google.colab || {};\n",
              "scope.google.colab._files = {\n",
              "  _uploadFiles,\n",
              "  _uploadFilesContinue,\n",
              "};\n",
              "})(self);\n",
              "</script> "
            ]
          },
          "metadata": {}
        },
        {
          "output_type": "stream",
          "name": "stdout",
          "text": [
            "Saving iiot_30min_norm.csv to iiot_30min_norm.csv\n"
          ]
        }
      ],
      "source": [
        "upload=files .upload ()"
      ]
    },
    {
      "cell_type": "code",
      "execution_count": null,
      "metadata": {
        "id": "A1w2uuW3mutk"
      },
      "outputs": [],
      "source": [
        "file_name = list(upload.keys())[0]\n",
        "df=pd.read_csv(file_name)"
      ]
    },
    {
      "cell_type": "code",
      "execution_count": null,
      "metadata": {
        "colab": {
          "base_uri": "https://localhost:8080/",
          "height": 424
        },
        "id": "Gg8SKjSJnHuS",
        "outputId": "f0b9eb00-3f3f-4991-ad2a-4f39882eade6"
      },
      "outputs": [
        {
          "output_type": "execute_result",
          "data": {
            "text/plain": [
              "                          TIME       FM1       PE1       PE2       PE3  \\\n",
              "0    2020-07-05 21:00:00+00:00  0.291841  0.944212  0.969845  0.909817   \n",
              "1    2020-07-05 21:30:00+00:00  0.290384  0.947971  0.971459  0.913576   \n",
              "2    2020-07-05 22:00:00+00:00  0.279458  0.944138  0.968994  0.912516   \n",
              "3    2020-07-05 22:30:00+00:00  0.288927  0.950337  0.976253  0.915991   \n",
              "4    2020-07-05 23:00:00+00:00  0.299610  0.950226  0.975747  0.916188   \n",
              "..                         ...       ...       ...       ...       ...   \n",
              "715  2020-07-20 18:30:00+00:00  0.509871  0.926097  0.954982  0.902386   \n",
              "716  2020-07-20 19:00:00+00:00  0.494696  0.925443  0.952851  0.902522   \n",
              "717  2020-07-20 19:30:00+00:00  0.483042  0.927908  0.953430  0.902238   \n",
              "718  2020-07-20 20:00:00+00:00  0.495382  0.925821  0.952846  0.899702   \n",
              "719  2020-07-20 20:30:00+00:00  0.495130  0.924763  0.948993  0.903162   \n",
              "\n",
              "          PE4       TP1       TP2       EPOCH  \n",
              "0    0.752879  0.128703  0.729592  1593982800  \n",
              "1    0.753741  0.117572  0.723905  1593984600  \n",
              "2    0.753187  0.111242  0.720671  1593986400  \n",
              "3    0.756699  0.102464  0.716186  1593988200  \n",
              "4    0.756563  0.093201  0.711454  1593990000  \n",
              "..        ...       ...       ...         ...  \n",
              "715  0.827435  0.459539  0.611203  1595269800  \n",
              "716  0.825390  0.429196  0.602910  1595271600  \n",
              "717  0.827238  0.355604  0.584250  1595273300  \n",
              "718  0.824158  0.325662  0.559331  1595275300  \n",
              "719  0.826645  0.298095  0.548365  1595277000  \n",
              "\n",
              "[720 rows x 9 columns]"
            ],
            "text/html": [
              "\n",
              "  <div id=\"df-d5a1678c-da80-4fa7-b9c6-f385b40d85a0\" class=\"colab-df-container\">\n",
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
              "      <th>TIME</th>\n",
              "      <th>FM1</th>\n",
              "      <th>PE1</th>\n",
              "      <th>PE2</th>\n",
              "      <th>PE3</th>\n",
              "      <th>PE4</th>\n",
              "      <th>TP1</th>\n",
              "      <th>TP2</th>\n",
              "      <th>EPOCH</th>\n",
              "    </tr>\n",
              "  </thead>\n",
              "  <tbody>\n",
              "    <tr>\n",
              "      <th>0</th>\n",
              "      <td>2020-07-05 21:00:00+00:00</td>\n",
              "      <td>0.291841</td>\n",
              "      <td>0.944212</td>\n",
              "      <td>0.969845</td>\n",
              "      <td>0.909817</td>\n",
              "      <td>0.752879</td>\n",
              "      <td>0.128703</td>\n",
              "      <td>0.729592</td>\n",
              "      <td>1593982800</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>1</th>\n",
              "      <td>2020-07-05 21:30:00+00:00</td>\n",
              "      <td>0.290384</td>\n",
              "      <td>0.947971</td>\n",
              "      <td>0.971459</td>\n",
              "      <td>0.913576</td>\n",
              "      <td>0.753741</td>\n",
              "      <td>0.117572</td>\n",
              "      <td>0.723905</td>\n",
              "      <td>1593984600</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>2</th>\n",
              "      <td>2020-07-05 22:00:00+00:00</td>\n",
              "      <td>0.279458</td>\n",
              "      <td>0.944138</td>\n",
              "      <td>0.968994</td>\n",
              "      <td>0.912516</td>\n",
              "      <td>0.753187</td>\n",
              "      <td>0.111242</td>\n",
              "      <td>0.720671</td>\n",
              "      <td>1593986400</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>3</th>\n",
              "      <td>2020-07-05 22:30:00+00:00</td>\n",
              "      <td>0.288927</td>\n",
              "      <td>0.950337</td>\n",
              "      <td>0.976253</td>\n",
              "      <td>0.915991</td>\n",
              "      <td>0.756699</td>\n",
              "      <td>0.102464</td>\n",
              "      <td>0.716186</td>\n",
              "      <td>1593988200</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>4</th>\n",
              "      <td>2020-07-05 23:00:00+00:00</td>\n",
              "      <td>0.299610</td>\n",
              "      <td>0.950226</td>\n",
              "      <td>0.975747</td>\n",
              "      <td>0.916188</td>\n",
              "      <td>0.756563</td>\n",
              "      <td>0.093201</td>\n",
              "      <td>0.711454</td>\n",
              "      <td>1593990000</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>...</th>\n",
              "      <td>...</td>\n",
              "      <td>...</td>\n",
              "      <td>...</td>\n",
              "      <td>...</td>\n",
              "      <td>...</td>\n",
              "      <td>...</td>\n",
              "      <td>...</td>\n",
              "      <td>...</td>\n",
              "      <td>...</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>715</th>\n",
              "      <td>2020-07-20 18:30:00+00:00</td>\n",
              "      <td>0.509871</td>\n",
              "      <td>0.926097</td>\n",
              "      <td>0.954982</td>\n",
              "      <td>0.902386</td>\n",
              "      <td>0.827435</td>\n",
              "      <td>0.459539</td>\n",
              "      <td>0.611203</td>\n",
              "      <td>1595269800</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>716</th>\n",
              "      <td>2020-07-20 19:00:00+00:00</td>\n",
              "      <td>0.494696</td>\n",
              "      <td>0.925443</td>\n",
              "      <td>0.952851</td>\n",
              "      <td>0.902522</td>\n",
              "      <td>0.825390</td>\n",
              "      <td>0.429196</td>\n",
              "      <td>0.602910</td>\n",
              "      <td>1595271600</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>717</th>\n",
              "      <td>2020-07-20 19:30:00+00:00</td>\n",
              "      <td>0.483042</td>\n",
              "      <td>0.927908</td>\n",
              "      <td>0.953430</td>\n",
              "      <td>0.902238</td>\n",
              "      <td>0.827238</td>\n",
              "      <td>0.355604</td>\n",
              "      <td>0.584250</td>\n",
              "      <td>1595273300</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>718</th>\n",
              "      <td>2020-07-20 20:00:00+00:00</td>\n",
              "      <td>0.495382</td>\n",
              "      <td>0.925821</td>\n",
              "      <td>0.952846</td>\n",
              "      <td>0.899702</td>\n",
              "      <td>0.824158</td>\n",
              "      <td>0.325662</td>\n",
              "      <td>0.559331</td>\n",
              "      <td>1595275300</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>719</th>\n",
              "      <td>2020-07-20 20:30:00+00:00</td>\n",
              "      <td>0.495130</td>\n",
              "      <td>0.924763</td>\n",
              "      <td>0.948993</td>\n",
              "      <td>0.903162</td>\n",
              "      <td>0.826645</td>\n",
              "      <td>0.298095</td>\n",
              "      <td>0.548365</td>\n",
              "      <td>1595277000</td>\n",
              "    </tr>\n",
              "  </tbody>\n",
              "</table>\n",
              "<p>720 rows × 9 columns</p>\n",
              "</div>\n",
              "    <div class=\"colab-df-buttons\">\n",
              "\n",
              "  <div class=\"colab-df-container\">\n",
              "    <button class=\"colab-df-convert\" onclick=\"convertToInteractive('df-d5a1678c-da80-4fa7-b9c6-f385b40d85a0')\"\n",
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
              "        document.querySelector('#df-d5a1678c-da80-4fa7-b9c6-f385b40d85a0 button.colab-df-convert');\n",
              "      buttonEl.style.display =\n",
              "        google.colab.kernel.accessAllowed ? 'block' : 'none';\n",
              "\n",
              "      async function convertToInteractive(key) {\n",
              "        const element = document.querySelector('#df-d5a1678c-da80-4fa7-b9c6-f385b40d85a0');\n",
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
              "    <div id=\"df-2432102f-5986-44b8-8b37-0deb09f2dbfe\">\n",
              "      <button class=\"colab-df-quickchart\" onclick=\"quickchart('df-2432102f-5986-44b8-8b37-0deb09f2dbfe')\"\n",
              "                title=\"Suggest charts\"\n",
              "                style=\"display:none;\">\n",
              "\n",
              "<svg xmlns=\"http://www.w3.org/2000/svg\" height=\"24px\"viewBox=\"0 0 24 24\"\n",
              "     width=\"24px\">\n",
              "    <g>\n",
              "        <path d=\"M19 3H5c-1.1 0-2 .9-2 2v14c0 1.1.9 2 2 2h14c1.1 0 2-.9 2-2V5c0-1.1-.9-2-2-2zM9 17H7v-7h2v7zm4 0h-2V7h2v10zm4 0h-2v-4h2v4z\"/>\n",
              "    </g>\n",
              "</svg>\n",
              "      </button>\n",
              "\n",
              "<style>\n",
              "  .colab-df-quickchart {\n",
              "      --bg-color: #E8F0FE;\n",
              "      --fill-color: #1967D2;\n",
              "      --hover-bg-color: #E2EBFA;\n",
              "      --hover-fill-color: #174EA6;\n",
              "      --disabled-fill-color: #AAA;\n",
              "      --disabled-bg-color: #DDD;\n",
              "  }\n",
              "\n",
              "  [theme=dark] .colab-df-quickchart {\n",
              "      --bg-color: #3B4455;\n",
              "      --fill-color: #D2E3FC;\n",
              "      --hover-bg-color: #434B5C;\n",
              "      --hover-fill-color: #FFFFFF;\n",
              "      --disabled-bg-color: #3B4455;\n",
              "      --disabled-fill-color: #666;\n",
              "  }\n",
              "\n",
              "  .colab-df-quickchart {\n",
              "    background-color: var(--bg-color);\n",
              "    border: none;\n",
              "    border-radius: 50%;\n",
              "    cursor: pointer;\n",
              "    display: none;\n",
              "    fill: var(--fill-color);\n",
              "    height: 32px;\n",
              "    padding: 0;\n",
              "    width: 32px;\n",
              "  }\n",
              "\n",
              "  .colab-df-quickchart:hover {\n",
              "    background-color: var(--hover-bg-color);\n",
              "    box-shadow: 0 1px 2px rgba(60, 64, 67, 0.3), 0 1px 3px 1px rgba(60, 64, 67, 0.15);\n",
              "    fill: var(--button-hover-fill-color);\n",
              "  }\n",
              "\n",
              "  .colab-df-quickchart-complete:disabled,\n",
              "  .colab-df-quickchart-complete:disabled:hover {\n",
              "    background-color: var(--disabled-bg-color);\n",
              "    fill: var(--disabled-fill-color);\n",
              "    box-shadow: none;\n",
              "  }\n",
              "\n",
              "  .colab-df-spinner {\n",
              "    border: 2px solid var(--fill-color);\n",
              "    border-color: transparent;\n",
              "    border-bottom-color: var(--fill-color);\n",
              "    animation:\n",
              "      spin 1s steps(1) infinite;\n",
              "  }\n",
              "\n",
              "  @keyframes spin {\n",
              "    0% {\n",
              "      border-color: transparent;\n",
              "      border-bottom-color: var(--fill-color);\n",
              "      border-left-color: var(--fill-color);\n",
              "    }\n",
              "    20% {\n",
              "      border-color: transparent;\n",
              "      border-left-color: var(--fill-color);\n",
              "      border-top-color: var(--fill-color);\n",
              "    }\n",
              "    30% {\n",
              "      border-color: transparent;\n",
              "      border-left-color: var(--fill-color);\n",
              "      border-top-color: var(--fill-color);\n",
              "      border-right-color: var(--fill-color);\n",
              "    }\n",
              "    40% {\n",
              "      border-color: transparent;\n",
              "      border-right-color: var(--fill-color);\n",
              "      border-top-color: var(--fill-color);\n",
              "    }\n",
              "    60% {\n",
              "      border-color: transparent;\n",
              "      border-right-color: var(--fill-color);\n",
              "    }\n",
              "    80% {\n",
              "      border-color: transparent;\n",
              "      border-right-color: var(--fill-color);\n",
              "      border-bottom-color: var(--fill-color);\n",
              "    }\n",
              "    90% {\n",
              "      border-color: transparent;\n",
              "      border-bottom-color: var(--fill-color);\n",
              "    }\n",
              "  }\n",
              "</style>\n",
              "\n",
              "      <script>\n",
              "        async function quickchart(key) {\n",
              "          const quickchartButtonEl =\n",
              "            document.querySelector('#' + key + ' button');\n",
              "          quickchartButtonEl.disabled = true;  // To prevent multiple clicks.\n",
              "          quickchartButtonEl.classList.add('colab-df-spinner');\n",
              "          try {\n",
              "            const charts = await google.colab.kernel.invokeFunction(\n",
              "                'suggestCharts', [key], {});\n",
              "          } catch (error) {\n",
              "            console.error('Error during call to suggestCharts:', error);\n",
              "          }\n",
              "          quickchartButtonEl.classList.remove('colab-df-spinner');\n",
              "          quickchartButtonEl.classList.add('colab-df-quickchart-complete');\n",
              "        }\n",
              "        (() => {\n",
              "          let quickchartButtonEl =\n",
              "            document.querySelector('#df-2432102f-5986-44b8-8b37-0deb09f2dbfe button');\n",
              "          quickchartButtonEl.style.display =\n",
              "            google.colab.kernel.accessAllowed ? 'block' : 'none';\n",
              "        })();\n",
              "      </script>\n",
              "    </div>\n",
              "\n",
              "  <div id=\"id_b66463f4-e2e7-4bbc-b200-62878a84f3ed\">\n",
              "    <style>\n",
              "      .colab-df-generate {\n",
              "        background-color: #E8F0FE;\n",
              "        border: none;\n",
              "        border-radius: 50%;\n",
              "        cursor: pointer;\n",
              "        display: none;\n",
              "        fill: #1967D2;\n",
              "        height: 32px;\n",
              "        padding: 0 0 0 0;\n",
              "        width: 32px;\n",
              "      }\n",
              "\n",
              "      .colab-df-generate:hover {\n",
              "        background-color: #E2EBFA;\n",
              "        box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);\n",
              "        fill: #174EA6;\n",
              "      }\n",
              "\n",
              "      [theme=dark] .colab-df-generate {\n",
              "        background-color: #3B4455;\n",
              "        fill: #D2E3FC;\n",
              "      }\n",
              "\n",
              "      [theme=dark] .colab-df-generate:hover {\n",
              "        background-color: #434B5C;\n",
              "        box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);\n",
              "        filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));\n",
              "        fill: #FFFFFF;\n",
              "      }\n",
              "    </style>\n",
              "    <button class=\"colab-df-generate\" onclick=\"generateWithVariable('df')\"\n",
              "            title=\"Generate code using this dataframe.\"\n",
              "            style=\"display:none;\">\n",
              "\n",
              "  <svg xmlns=\"http://www.w3.org/2000/svg\" height=\"24px\"viewBox=\"0 0 24 24\"\n",
              "       width=\"24px\">\n",
              "    <path d=\"M7,19H8.4L18.45,9,17,7.55,7,17.6ZM5,21V16.75L18.45,3.32a2,2,0,0,1,2.83,0l1.4,1.43a1.91,1.91,0,0,1,.58,1.4,1.91,1.91,0,0,1-.58,1.4L9.25,21ZM18.45,9,17,7.55Zm-12,3A5.31,5.31,0,0,0,4.9,8.1,5.31,5.31,0,0,0,1,6.5,5.31,5.31,0,0,0,4.9,4.9,5.31,5.31,0,0,0,6.5,1,5.31,5.31,0,0,0,8.1,4.9,5.31,5.31,0,0,0,12,6.5,5.46,5.46,0,0,0,6.5,12Z\"/>\n",
              "  </svg>\n",
              "    </button>\n",
              "    <script>\n",
              "      (() => {\n",
              "      const buttonEl =\n",
              "        document.querySelector('#id_b66463f4-e2e7-4bbc-b200-62878a84f3ed button.colab-df-generate');\n",
              "      buttonEl.style.display =\n",
              "        google.colab.kernel.accessAllowed ? 'block' : 'none';\n",
              "\n",
              "      buttonEl.onclick = () => {\n",
              "        google.colab.notebook.generateWithVariable('df');\n",
              "      }\n",
              "      })();\n",
              "    </script>\n",
              "  </div>\n",
              "\n",
              "    </div>\n",
              "  </div>\n"
            ],
            "application/vnd.google.colaboratory.intrinsic+json": {
              "type": "dataframe",
              "variable_name": "df",
              "summary": "{\n  \"name\": \"df\",\n  \"rows\": 720,\n  \"fields\": [\n    {\n      \"column\": \"TIME\",\n      \"properties\": {\n        \"dtype\": \"object\",\n        \"num_unique_values\": 720,\n        \"samples\": [\n          \"2020-07-12 23:00:00+00:00\",\n          \"2020-07-11 22:00:00+00:00\",\n          \"2020-07-07 00:00:00+00:00\"\n        ],\n        \"semantic_type\": \"\",\n        \"description\": \"\"\n      }\n    },\n    {\n      \"column\": \"FM1\",\n      \"properties\": {\n        \"dtype\": \"number\",\n        \"std\": 0.113317365095595,\n        \"min\": 0.0,\n        \"max\": 1.0,\n        \"num_unique_values\": 664,\n        \"samples\": [\n          0.34404168,\n          0.34477007,\n          0.36237276\n        ],\n        \"semantic_type\": \"\",\n        \"description\": \"\"\n      }\n    },\n    {\n      \"column\": \"PE1\",\n      \"properties\": {\n        \"dtype\": \"number\",\n        \"std\": 0.00689592564708434,\n        \"min\": 0.922572,\n        \"max\": 0.9744536,\n        \"num_unique_values\": 609,\n        \"samples\": [\n          0.94307816,\n          0.9277971,\n          0.9417102\n        ],\n        \"semantic_type\": \"\",\n        \"description\": \"\"\n      }\n    },\n    {\n      \"column\": \"PE2\",\n      \"properties\": {\n        \"dtype\": \"number\",\n        \"std\": 0.038904147920629864,\n        \"min\": 0.27706966,\n        \"max\": 1.0,\n        \"num_unique_values\": 625,\n        \"samples\": [\n          0.9535899,\n          0.9641758,\n          0.9638431\n        ],\n        \"semantic_type\": \"\",\n        \"description\": \"\"\n      }\n    },\n    {\n      \"column\": \"PE3\",\n      \"properties\": {\n        \"dtype\": \"number\",\n        \"std\": 0.04209306094117432,\n        \"min\": 0.023603452,\n        \"max\": 0.944446,\n        \"num_unique_values\": 651,\n        \"samples\": [\n          0.9023122,\n          0.90904087,\n          0.9139702\n        ],\n        \"semantic_type\": \"\",\n        \"description\": \"\"\n      }\n    },\n    {\n      \"column\": \"PE4\",\n      \"properties\": {\n        \"dtype\": \"number\",\n        \"std\": 0.05131375829629446,\n        \"min\": 0.0,\n        \"max\": 0.8401407,\n        \"num_unique_values\": 680,\n        \"samples\": [\n          0.7803061,\n          0.7864792,\n          0.80859685\n        ],\n        \"semantic_type\": \"\",\n        \"description\": \"\"\n      }\n    },\n    {\n      \"column\": \"TP1\",\n      \"properties\": {\n        \"dtype\": \"number\",\n        \"std\": 0.21711963517721278,\n        \"min\": 0.0,\n        \"max\": 1.0,\n        \"num_unique_values\": 572,\n        \"samples\": [\n          0.80743235,\n          0.28935546,\n          0.2838994\n        ],\n        \"semantic_type\": \"\",\n        \"description\": \"\"\n      }\n    },\n    {\n      \"column\": \"TP2\",\n      \"properties\": {\n        \"dtype\": \"number\",\n        \"std\": 0.13840251316697605,\n        \"min\": 0.0,\n        \"max\": 1.0,\n        \"num_unique_values\": 605,\n        \"samples\": [\n          0.69775426,\n          0.4917079,\n          0.7863855\n        ],\n        \"semantic_type\": \"\",\n        \"description\": \"\"\n      }\n    },\n    {\n      \"column\": \"EPOCH\",\n      \"properties\": {\n        \"dtype\": \"number\",\n        \"std\": 374382,\n        \"min\": 1593982800,\n        \"max\": 1595277000,\n        \"num_unique_values\": 720,\n        \"samples\": [\n          1594594800,\n          1594504800,\n          1594080000\n        ],\n        \"semantic_type\": \"\",\n        \"description\": \"\"\n      }\n    }\n  ]\n}"
            }
          },
          "metadata": {},
          "execution_count": 7
        }
      ],
      "source": [
        "df"
      ]
    },
    {
      "cell_type": "code",
      "execution_count": null,
      "metadata": {
        "colab": {
          "base_uri": "https://localhost:8080/"
        },
        "id": "01eJ6869nRrd",
        "outputId": "157701e9-6ca2-42bd-fd00-2cde20448696"
      },
      "outputs": [
        {
          "output_type": "execute_result",
          "data": {
            "text/plain": [
              "(720, 9)"
            ]
          },
          "metadata": {},
          "execution_count": 8
        }
      ],
      "source": [
        "df. shape"
      ]
    },
    {
      "cell_type": "code",
      "execution_count": null,
      "metadata": {
        "colab": {
          "base_uri": "https://localhost:8080/",
          "height": 204
        },
        "id": "5Llyzo-Fn5wK",
        "outputId": "65a4b4d6-05f0-45aa-bcb2-ef135aab0b20"
      },
      "outputs": [
        {
          "output_type": "execute_result",
          "data": {
            "text/plain": [
              "<bound method DataFrame.info of                           TIME       FM1       PE1       PE2       PE3  \\\n",
              "0    2020-07-05 21:00:00+00:00  0.291841  0.944212  0.969845  0.909817   \n",
              "1    2020-07-05 21:30:00+00:00  0.290384  0.947971  0.971459  0.913576   \n",
              "2    2020-07-05 22:00:00+00:00  0.279458  0.944138  0.968994  0.912516   \n",
              "3    2020-07-05 22:30:00+00:00  0.288927  0.950337  0.976253  0.915991   \n",
              "4    2020-07-05 23:00:00+00:00  0.299610  0.950226  0.975747  0.916188   \n",
              "..                         ...       ...       ...       ...       ...   \n",
              "715  2020-07-20 18:30:00+00:00  0.509871  0.926097  0.954982  0.902386   \n",
              "716  2020-07-20 19:00:00+00:00  0.494696  0.925443  0.952851  0.902522   \n",
              "717  2020-07-20 19:30:00+00:00  0.483042  0.927908  0.953430  0.902238   \n",
              "718  2020-07-20 20:00:00+00:00  0.495382  0.925821  0.952846  0.899702   \n",
              "719  2020-07-20 20:30:00+00:00  0.495130  0.924763  0.948993  0.903162   \n",
              "\n",
              "          PE4       TP1       TP2       EPOCH  \n",
              "0    0.752879  0.128703  0.729592  1593982800  \n",
              "1    0.753741  0.117572  0.723905  1593984600  \n",
              "2    0.753187  0.111242  0.720671  1593986400  \n",
              "3    0.756699  0.102464  0.716186  1593988200  \n",
              "4    0.756563  0.093201  0.711454  1593990000  \n",
              "..        ...       ...       ...         ...  \n",
              "715  0.827435  0.459539  0.611203  1595269800  \n",
              "716  0.825390  0.429196  0.602910  1595271600  \n",
              "717  0.827238  0.355604  0.584250  1595273300  \n",
              "718  0.824158  0.325662  0.559331  1595275300  \n",
              "719  0.826645  0.298095  0.548365  1595277000  \n",
              "\n",
              "[720 rows x 9 columns]>"
            ],
            "text/html": [
              "<div style=\"max-width:800px; border: 1px solid var(--colab-border-color);\"><style>\n",
              "      pre.function-repr-contents {\n",
              "        overflow-x: auto;\n",
              "        padding: 8px 12px;\n",
              "        max-height: 500px;\n",
              "      }\n",
              "\n",
              "      pre.function-repr-contents.function-repr-contents-collapsed {\n",
              "        cursor: pointer;\n",
              "        max-height: 100px;\n",
              "      }\n",
              "    </style>\n",
              "    <pre style=\"white-space: initial; background:\n",
              "         var(--colab-secondary-surface-color); padding: 8px 12px;\n",
              "         border-bottom: 1px solid var(--colab-border-color);\"><b>pandas.core.frame.DataFrame.info</b><br/>def info(verbose: bool | None=None, buf: WriteBuffer[str] | None=None, max_cols: int | None=None, memory_usage: bool | str | None=None, show_counts: bool | None=None) -&gt; None</pre><pre class=\"function-repr-contents function-repr-contents-collapsed\" style=\"\"><a class=\"filepath\" style=\"display:none\" href=\"#\">/usr/local/lib/python3.12/dist-packages/pandas/core/frame.py</a>Print a concise summary of a DataFrame.\n",
              "\n",
              "This method prints information about a DataFrame including\n",
              "the index dtype and columns, non-null values and memory usage.\n",
              "\n",
              "Parameters\n",
              "----------\n",
              "verbose : bool, optional\n",
              "    Whether to print the full summary. By default, the setting in\n",
              "    ``pandas.options.display.max_info_columns`` is followed.\n",
              "buf : writable buffer, defaults to sys.stdout\n",
              "    Where to send the output. By default, the output is printed to\n",
              "    sys.stdout. Pass a writable buffer if you need to further process\n",
              "    the output.\n",
              "max_cols : int, optional\n",
              "    When to switch from the verbose to the truncated output. If the\n",
              "    DataFrame has more than `max_cols` columns, the truncated output\n",
              "    is used. By default, the setting in\n",
              "    ``pandas.options.display.max_info_columns`` is used.\n",
              "memory_usage : bool, str, optional\n",
              "    Specifies whether total memory usage of the DataFrame\n",
              "    elements (including the index) should be displayed. By default,\n",
              "    this follows the ``pandas.options.display.memory_usage`` setting.\n",
              "\n",
              "    True always show memory usage. False never shows memory usage.\n",
              "    A value of &#x27;deep&#x27; is equivalent to &quot;True with deep introspection&quot;.\n",
              "    Memory usage is shown in human-readable units (base-2\n",
              "    representation). Without deep introspection a memory estimation is\n",
              "    made based in column dtype and number of rows assuming values\n",
              "    consume the same memory amount for corresponding dtypes. With deep\n",
              "    memory introspection, a real memory usage calculation is performed\n",
              "    at the cost of computational resources. See the\n",
              "    :ref:`Frequently Asked Questions &lt;df-memory-usage&gt;` for more\n",
              "    details.\n",
              "show_counts : bool, optional\n",
              "    Whether to show the non-null counts. By default, this is shown\n",
              "    only if the DataFrame is smaller than\n",
              "    ``pandas.options.display.max_info_rows`` and\n",
              "    ``pandas.options.display.max_info_columns``. A value of True always\n",
              "    shows the counts, and False never shows the counts.\n",
              "\n",
              "Returns\n",
              "-------\n",
              "None\n",
              "    This method prints a summary of a DataFrame and returns None.\n",
              "\n",
              "See Also\n",
              "--------\n",
              "DataFrame.describe: Generate descriptive statistics of DataFrame\n",
              "    columns.\n",
              "DataFrame.memory_usage: Memory usage of DataFrame columns.\n",
              "\n",
              "Examples\n",
              "--------\n",
              "&gt;&gt;&gt; int_values = [1, 2, 3, 4, 5]\n",
              "&gt;&gt;&gt; text_values = [&#x27;alpha&#x27;, &#x27;beta&#x27;, &#x27;gamma&#x27;, &#x27;delta&#x27;, &#x27;epsilon&#x27;]\n",
              "&gt;&gt;&gt; float_values = [0.0, 0.25, 0.5, 0.75, 1.0]\n",
              "&gt;&gt;&gt; df = pd.DataFrame({&quot;int_col&quot;: int_values, &quot;text_col&quot;: text_values,\n",
              "...                   &quot;float_col&quot;: float_values})\n",
              "&gt;&gt;&gt; df\n",
              "    int_col text_col  float_col\n",
              "0        1    alpha       0.00\n",
              "1        2     beta       0.25\n",
              "2        3    gamma       0.50\n",
              "3        4    delta       0.75\n",
              "4        5  epsilon       1.00\n",
              "\n",
              "Prints information of all columns:\n",
              "\n",
              "&gt;&gt;&gt; df.info(verbose=True)\n",
              "&lt;class &#x27;pandas.core.frame.DataFrame&#x27;&gt;\n",
              "RangeIndex: 5 entries, 0 to 4\n",
              "Data columns (total 3 columns):\n",
              " #   Column     Non-Null Count  Dtype\n",
              "---  ------     --------------  -----\n",
              " 0   int_col    5 non-null      int64\n",
              " 1   text_col   5 non-null      object\n",
              " 2   float_col  5 non-null      float64\n",
              "dtypes: float64(1), int64(1), object(1)\n",
              "memory usage: 248.0+ bytes\n",
              "\n",
              "Prints a summary of columns count and its dtypes but not per column\n",
              "information:\n",
              "\n",
              "&gt;&gt;&gt; df.info(verbose=False)\n",
              "&lt;class &#x27;pandas.core.frame.DataFrame&#x27;&gt;\n",
              "RangeIndex: 5 entries, 0 to 4\n",
              "Columns: 3 entries, int_col to float_col\n",
              "dtypes: float64(1), int64(1), object(1)\n",
              "memory usage: 248.0+ bytes\n",
              "\n",
              "Pipe output of DataFrame.info to buffer instead of sys.stdout, get\n",
              "buffer content and writes to a text file:\n",
              "\n",
              "&gt;&gt;&gt; import io\n",
              "&gt;&gt;&gt; buffer = io.StringIO()\n",
              "&gt;&gt;&gt; df.info(buf=buffer)\n",
              "&gt;&gt;&gt; s = buffer.getvalue()\n",
              "&gt;&gt;&gt; with open(&quot;df_info.txt&quot;, &quot;w&quot;,\n",
              "...           encoding=&quot;utf-8&quot;) as f:  # doctest: +SKIP\n",
              "...     f.write(s)\n",
              "260\n",
              "\n",
              "The `memory_usage` parameter allows deep introspection mode, specially\n",
              "useful for big DataFrames and fine-tune memory optimization:\n",
              "\n",
              "&gt;&gt;&gt; random_strings_array = np.random.choice([&#x27;a&#x27;, &#x27;b&#x27;, &#x27;c&#x27;], 10 ** 6)\n",
              "&gt;&gt;&gt; df = pd.DataFrame({\n",
              "...     &#x27;column_1&#x27;: np.random.choice([&#x27;a&#x27;, &#x27;b&#x27;, &#x27;c&#x27;], 10 ** 6),\n",
              "...     &#x27;column_2&#x27;: np.random.choice([&#x27;a&#x27;, &#x27;b&#x27;, &#x27;c&#x27;], 10 ** 6),\n",
              "...     &#x27;column_3&#x27;: np.random.choice([&#x27;a&#x27;, &#x27;b&#x27;, &#x27;c&#x27;], 10 ** 6)\n",
              "... })\n",
              "&gt;&gt;&gt; df.info()\n",
              "&lt;class &#x27;pandas.core.frame.DataFrame&#x27;&gt;\n",
              "RangeIndex: 1000000 entries, 0 to 999999\n",
              "Data columns (total 3 columns):\n",
              " #   Column    Non-Null Count    Dtype\n",
              "---  ------    --------------    -----\n",
              " 0   column_1  1000000 non-null  object\n",
              " 1   column_2  1000000 non-null  object\n",
              " 2   column_3  1000000 non-null  object\n",
              "dtypes: object(3)\n",
              "memory usage: 22.9+ MB\n",
              "\n",
              "&gt;&gt;&gt; df.info(memory_usage=&#x27;deep&#x27;)\n",
              "&lt;class &#x27;pandas.core.frame.DataFrame&#x27;&gt;\n",
              "RangeIndex: 1000000 entries, 0 to 999999\n",
              "Data columns (total 3 columns):\n",
              " #   Column    Non-Null Count    Dtype\n",
              "---  ------    --------------    -----\n",
              " 0   column_1  1000000 non-null  object\n",
              " 1   column_2  1000000 non-null  object\n",
              " 2   column_3  1000000 non-null  object\n",
              "dtypes: object(3)\n",
              "memory usage: 165.9 MB</pre>\n",
              "      <script>\n",
              "      if (google.colab.kernel.accessAllowed && google.colab.files && google.colab.files.view) {\n",
              "        for (const element of document.querySelectorAll('.filepath')) {\n",
              "          element.style.display = 'block'\n",
              "          element.onclick = (event) => {\n",
              "            event.preventDefault();\n",
              "            event.stopPropagation();\n",
              "            google.colab.files.view(element.textContent, 3646);\n",
              "          };\n",
              "        }\n",
              "      }\n",
              "      for (const element of document.querySelectorAll('.function-repr-contents')) {\n",
              "        element.onclick = (event) => {\n",
              "          event.preventDefault();\n",
              "          event.stopPropagation();\n",
              "          element.classList.toggle('function-repr-contents-collapsed');\n",
              "        };\n",
              "      }\n",
              "      </script>\n",
              "      </div>"
            ]
          },
          "metadata": {},
          "execution_count": 9
        }
      ],
      "source": [
        "df.info"
      ]
    },
    {
      "cell_type": "code",
      "execution_count": null,
      "metadata": {
        "colab": {
          "base_uri": "https://localhost:8080/",
          "height": 366
        },
        "id": "U83YssgBoCpg",
        "outputId": "08758137-326a-4e4d-d86f-d682b33ba8bc"
      },
      "outputs": [
        {
          "output_type": "execute_result",
          "data": {
            "text/plain": [
              "TIME     0\n",
              "FM1      0\n",
              "PE1      0\n",
              "PE2      0\n",
              "PE3      0\n",
              "PE4      0\n",
              "TP1      0\n",
              "TP2      0\n",
              "EPOCH    0\n",
              "dtype: int64"
            ],
            "text/html": [
              "<div>\n",
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
              "      <th>0</th>\n",
              "    </tr>\n",
              "  </thead>\n",
              "  <tbody>\n",
              "    <tr>\n",
              "      <th>TIME</th>\n",
              "      <td>0</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>FM1</th>\n",
              "      <td>0</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>PE1</th>\n",
              "      <td>0</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>PE2</th>\n",
              "      <td>0</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>PE3</th>\n",
              "      <td>0</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>PE4</th>\n",
              "      <td>0</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>TP1</th>\n",
              "      <td>0</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>TP2</th>\n",
              "      <td>0</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>EPOCH</th>\n",
              "      <td>0</td>\n",
              "    </tr>\n",
              "  </tbody>\n",
              "</table>\n",
              "</div><br><label><b>dtype:</b> int64</label>"
            ]
          },
          "metadata": {},
          "execution_count": 12
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
        "id": "2EYBWYelogxB"
      },
      "outputs": [],
      "source": [
        "df_clean=df.copy()"
      ]
    },
    {
      "cell_type": "code",
      "execution_count": null,
      "metadata": {
        "id": "rPHtkxAGox9K"
      },
      "outputs": [],
      "source": [
        "columns_to_drop = []"
      ]
    },
    {
      "cell_type": "code",
      "execution_count": null,
      "metadata": {
        "id": "6EIpejBso4jm"
      },
      "outputs": [],
      "source": [
        "for col in df_clean.columns:\n",
        "  if df_clean[col].isnull().sum()>len(df_clean)*0.5:\n",
        "    columns_to_drop.append(col)\n",
        "  elif df_clean[col].dtype ==\"object\" and col != 'TIME': # Exclude 'TIME' from dropping if it's an object\n",
        "    columns_to_drop.append(col)"
      ]
    },
    {
      "cell_type": "code",
      "execution_count": null,
      "metadata": {
        "colab": {
          "base_uri": "https://localhost:8080/"
        },
        "id": "1XIHEiqRqnO0",
        "outputId": "089d97b8-ed41-42e7-f53d-d63c1417f50d"
      },
      "outputs": [
        {
          "output_type": "execute_result",
          "data": {
            "text/plain": [
              "['TIME']"
            ]
          },
          "metadata": {},
          "execution_count": 17
        }
      ],
      "source": [
        "columns_to_drop"
      ]
    },
    {
      "cell_type": "code",
      "execution_count": null,
      "metadata": {
        "id": "F-zjFp8Hq47H"
      },
      "outputs": [],
      "source": [
        "# Convert all columns except 'TIME' to numeric, coercing errors\n",
        "for col in df_clean.columns:\n",
        "    if col != 'TIME':\n",
        "        df_clean[col] = pd.to_numeric(df_clean[col], errors=\"coerce\")\n",
        "\n",
        "# Convert 'TIME' to datetime objects\n",
        "df_clean['TIME'] = pd.to_datetime(df_clean['TIME'], errors='coerce', utc=True)"
      ]
    },
    {
      "cell_type": "code",
      "execution_count": null,
      "metadata": {
        "id": "9VVOk14LrXk9"
      },
      "outputs": [],
      "source": [
        "df_clean = df_clean.dropna(subset=[target]) # Drop rows where the target (TIME) is NaN"
      ]
    },
    {
      "cell_type": "code",
      "execution_count": null,
      "metadata": {
        "id": "ddb_5oRssEx2"
      },
      "outputs": [],
      "source": [
        "target=\"TIME\""
      ]
    },
    {
      "cell_type": "code",
      "execution_count": null,
      "metadata": {
        "id": "D1Q8lDHmspKe"
      },
      "outputs": [],
      "source": [
        "features=[col for col in df_clean.columns if col not in [target]]"
      ]
    },
    {
      "cell_type": "code",
      "execution_count": null,
      "metadata": {
        "colab": {
          "base_uri": "https://localhost:8080/"
        },
        "id": "K0ak7VrStLTT",
        "outputId": "f41de931-72ce-4418-bc58-39e43067d9be"
      },
      "outputs": [
        {
          "output_type": "execute_result",
          "data": {
            "text/plain": [
              "['FM1', 'PE1', 'PE2', 'PE3', 'PE4', 'TP1', 'TP2', 'EPOCH']"
            ]
          },
          "metadata": {},
          "execution_count": 22
        }
      ],
      "source": [
        "features"
      ]
    },
    {
      "cell_type": "code",
      "execution_count": null,
      "metadata": {
        "id": "9xoPu_l0tQjV"
      },
      "outputs": [],
      "source": [
        "x= df_clean [features]\n",
        "y=df_clean [target]"
      ]
    },
    {
      "cell_type": "code",
      "execution_count": null,
      "metadata": {
        "colab": {
          "base_uri": "https://localhost:8080/",
          "height": 84
        },
        "id": "YZFwkIsyth_L",
        "outputId": "2c1265bf-0d9a-466b-f219-48c63ec9f7c2"
      },
      "outputs": [
        {
          "output_type": "execute_result",
          "data": {
            "text/plain": [
              "Series([], Name: TIME, dtype: float64)"
            ],
            "text/html": [
              "<div>\n",
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
              "      <th>TIME</th>\n",
              "    </tr>\n",
              "  </thead>\n",
              "  <tbody>\n",
              "  </tbody>\n",
              "</table>\n",
              "</div><br><label><b>dtype:</b> float64</label>"
            ]
          },
          "metadata": {},
          "execution_count": 24
        }
      ],
      "source": [
        "y"
      ]
    },
    {
      "cell_type": "code",
      "execution_count": null,
      "metadata": {
        "id": "4O1w5IZDt1CS"
      },
      "outputs": [],
      "source": [
        "from sklearn.model_selection import train_test_split"
      ]
    },
    {
      "cell_type": "code",
      "execution_count": null,
      "metadata": {
        "colab": {
          "base_uri": "https://localhost:8080/",
          "height": 287
        },
        "id": "Y8pAcgopuPB1",
        "outputId": "be868782-3865-440e-d183-dd4bded0547d"
      },
      "outputs": [
        {
          "output_type": "error",
          "ename": "ValueError",
          "evalue": "With n_samples=0, test_size=0.2 and train_size=None, the resulting train set will be empty. Adjust any of the aforementioned parameters.",
          "traceback": [
            "\u001b[0;31m---------------------------------------------------------------------------\u001b[0m",
            "\u001b[0;31mValueError\u001b[0m                                Traceback (most recent call last)",
            "\u001b[0;32m/tmp/ipython-input-3388309346.py\u001b[0m in \u001b[0;36m<cell line: 0>\u001b[0;34m()\u001b[0m\n\u001b[0;32m----> 1\u001b[0;31m \u001b[0mx_train\u001b[0m\u001b[0;34m,\u001b[0m \u001b[0mx_test\u001b[0m\u001b[0;34m,\u001b[0m \u001b[0my_train\u001b[0m\u001b[0;34m,\u001b[0m \u001b[0my_test\u001b[0m \u001b[0;34m=\u001b[0m \u001b[0mtrain_test_split\u001b[0m\u001b[0;34m(\u001b[0m\u001b[0mx\u001b[0m\u001b[0;34m,\u001b[0m \u001b[0my\u001b[0m\u001b[0;34m,\u001b[0m \u001b[0mtest_size\u001b[0m\u001b[0;34m=\u001b[0m\u001b[0;36m0.2\u001b[0m\u001b[0;34m,\u001b[0m \u001b[0mrandom_state\u001b[0m\u001b[0;34m=\u001b[0m\u001b[0;36m42\u001b[0m\u001b[0;34m)\u001b[0m\u001b[0;34m\u001b[0m\u001b[0;34m\u001b[0m\u001b[0m\n\u001b[0m",
            "\u001b[0;32m/usr/local/lib/python3.12/dist-packages/sklearn/utils/_param_validation.py\u001b[0m in \u001b[0;36mwrapper\u001b[0;34m(*args, **kwargs)\u001b[0m\n\u001b[1;32m    214\u001b[0m                     )\n\u001b[1;32m    215\u001b[0m                 ):\n\u001b[0;32m--> 216\u001b[0;31m                     \u001b[0;32mreturn\u001b[0m \u001b[0mfunc\u001b[0m\u001b[0;34m(\u001b[0m\u001b[0;34m*\u001b[0m\u001b[0margs\u001b[0m\u001b[0;34m,\u001b[0m \u001b[0;34m**\u001b[0m\u001b[0mkwargs\u001b[0m\u001b[0;34m)\u001b[0m\u001b[0;34m\u001b[0m\u001b[0;34m\u001b[0m\u001b[0m\n\u001b[0m\u001b[1;32m    217\u001b[0m             \u001b[0;32mexcept\u001b[0m \u001b[0mInvalidParameterError\u001b[0m \u001b[0;32mas\u001b[0m \u001b[0me\u001b[0m\u001b[0;34m:\u001b[0m\u001b[0;34m\u001b[0m\u001b[0;34m\u001b[0m\u001b[0m\n\u001b[1;32m    218\u001b[0m                 \u001b[0;31m# When the function is just a wrapper around an estimator, we allow\u001b[0m\u001b[0;34m\u001b[0m\u001b[0;34m\u001b[0m\u001b[0m\n",
            "\u001b[0;32m/usr/local/lib/python3.12/dist-packages/sklearn/model_selection/_split.py\u001b[0m in \u001b[0;36mtrain_test_split\u001b[0;34m(test_size, train_size, random_state, shuffle, stratify, *arrays)\u001b[0m\n\u001b[1;32m   2849\u001b[0m \u001b[0;34m\u001b[0m\u001b[0m\n\u001b[1;32m   2850\u001b[0m     \u001b[0mn_samples\u001b[0m \u001b[0;34m=\u001b[0m \u001b[0m_num_samples\u001b[0m\u001b[0;34m(\u001b[0m\u001b[0marrays\u001b[0m\u001b[0;34m[\u001b[0m\u001b[0;36m0\u001b[0m\u001b[0;34m]\u001b[0m\u001b[0;34m)\u001b[0m\u001b[0;34m\u001b[0m\u001b[0;34m\u001b[0m\u001b[0m\n\u001b[0;32m-> 2851\u001b[0;31m     n_train, n_test = _validate_shuffle_split(\n\u001b[0m\u001b[1;32m   2852\u001b[0m         \u001b[0mn_samples\u001b[0m\u001b[0;34m,\u001b[0m \u001b[0mtest_size\u001b[0m\u001b[0;34m,\u001b[0m \u001b[0mtrain_size\u001b[0m\u001b[0;34m,\u001b[0m \u001b[0mdefault_test_size\u001b[0m\u001b[0;34m=\u001b[0m\u001b[0;36m0.25\u001b[0m\u001b[0;34m\u001b[0m\u001b[0;34m\u001b[0m\u001b[0m\n\u001b[1;32m   2853\u001b[0m     )\n",
            "\u001b[0;32m/usr/local/lib/python3.12/dist-packages/sklearn/model_selection/_split.py\u001b[0m in \u001b[0;36m_validate_shuffle_split\u001b[0;34m(n_samples, test_size, train_size, default_test_size)\u001b[0m\n\u001b[1;32m   2479\u001b[0m \u001b[0;34m\u001b[0m\u001b[0m\n\u001b[1;32m   2480\u001b[0m     \u001b[0;32mif\u001b[0m \u001b[0mn_train\u001b[0m \u001b[0;34m==\u001b[0m \u001b[0;36m0\u001b[0m\u001b[0;34m:\u001b[0m\u001b[0;34m\u001b[0m\u001b[0;34m\u001b[0m\u001b[0m\n\u001b[0;32m-> 2481\u001b[0;31m         raise ValueError(\n\u001b[0m\u001b[1;32m   2482\u001b[0m             \u001b[0;34m\"With n_samples={}, test_size={} and train_size={}, the \"\u001b[0m\u001b[0;34m\u001b[0m\u001b[0;34m\u001b[0m\u001b[0m\n\u001b[1;32m   2483\u001b[0m             \u001b[0;34m\"resulting train set will be empty. Adjust any of the \"\u001b[0m\u001b[0;34m\u001b[0m\u001b[0;34m\u001b[0m\u001b[0m\n",
            "\u001b[0;31mValueError\u001b[0m: With n_samples=0, test_size=0.2 and train_size=None, the resulting train set will be empty. Adjust any of the aforementioned parameters."
          ]
        }
      ],
      "source": [
        "x_train, x_test, y_train, y_test = train_test_split(x, y, test_size=0.2, random_state=42)"
      ]
    },
    {
      "cell_type": "code",
      "execution_count": null,
      "metadata": {
        "colab": {
          "base_uri": "https://localhost:8080/",
          "height": 141
        },
        "id": "DsJdnipdvUZq",
        "outputId": "da4c2ac7-6f31-4510-da82-8b16232fecba"
      },
      "outputs": [
        {
          "output_type": "error",
          "ename": "NameError",
          "evalue": "name 'x_train' is not defined",
          "traceback": [
            "\u001b[0;31m---------------------------------------------------------------------------\u001b[0m",
            "\u001b[0;31mNameError\u001b[0m                                 Traceback (most recent call last)",
            "\u001b[0;32m/tmp/ipython-input-182409954.py\u001b[0m in \u001b[0;36m<cell line: 0>\u001b[0;34m()\u001b[0m\n\u001b[0;32m----> 1\u001b[0;31m \u001b[0mx_train\u001b[0m\u001b[0;34m.\u001b[0m\u001b[0miloc\u001b[0m\u001b[0;34m[\u001b[0m\u001b[0;34m\"TIME\"\u001b[0m\u001b[0;34m]\u001b[0m\u001b[0;34m\u001b[0m\u001b[0;34m\u001b[0m\u001b[0m\n\u001b[0m",
            "\u001b[0;31mNameError\u001b[0m: name 'x_train' is not defined"
          ]
        }
      ],
      "source": [
        "x_train.iloc[\"TIME\"]"
      ]
    },
    {
      "cell_type": "code",
      "execution_count": null,
      "metadata": {
        "colab": {
          "base_uri": "https://localhost:8080/",
          "height": 106
        },
        "id": "tW843QVewB15",
        "outputId": "c4395edb-ad34-477e-cf9e-8976897ed0a8"
      },
      "outputs": [
        {
          "ename": "SyntaxError",
          "evalue": "invalid syntax (ipython-input-1943082584.py, line 1)",
          "output_type": "error",
          "traceback": [
            "\u001b[0;36m  File \u001b[0;32m\"/tmp/ipython-input-1943082584.py\"\u001b[0;36m, line \u001b[0;32m1\u001b[0m\n\u001b[0;31m    from sklearn, linear_model import LinearRegression\u001b[0m\n\u001b[0m                ^\u001b[0m\n\u001b[0;31mSyntaxError\u001b[0m\u001b[0;31m:\u001b[0m invalid syntax\n"
          ]
        }
      ],
      "source": [
        "from sklearn, linear_model import LinearRegression"
      ]
    },
    {
      "cell_type": "code",
      "execution_count": null,
      "metadata": {
        "id": "-QA2PG_SwylN"
      },
      "outputs": [],
      "source": [
        "sencillo= LinearRegression()\n"
      ]
    }
  ],
  "metadata": {
    "colab": {
      "provenance": [],
      "include_colab_link": true
    },
    "kernelspec": {
      "display_name": "Python 3",
      "name": "python3"
    }
  },
  "nbformat": 4,
  "nbformat_minor": 0
}
