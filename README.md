# The Starbucks Latte Index

![Pumpkin spice latte](picture.png "Pumpkin spice latte")

Have you ever wondered if your dollar is valued the same no matter what country you are in? Have you ever wondered if you actually get your money’s worth when buying goods in other countries?

# Purchasing Power Parity
Understanding purchasing power parity is crucial as it can help you answer these questions. It measures the differences in price levels between countries in that country’s currency. It helps you find an exchange rate based on price levels, which may be lower or higher than the nominal exchange rate set by the Bank of Canada. Having a higher PPP than the exchange rate means that you could buy coffee in another country cheaper than what you can buy in Canada.

To make this concept more tangible, we have created a Starbucks Tall Latte Index, which shows the prices of tall lattes in different countries. This index is a practical tool to understand the implications of purchasing power parity.

# Why Starbucks Latte?
Starbucks latte is a tasty, energizing drink that many people consume daily. Starbucks is one of the most recognizable coffee companies, with many locations worldwide. Additionally, consumers worldwide expect to drink the same latte in Canada, just as in Brazil. Similarly, consumers would expect their currency's value to be the same in other countries and afford a latte across different countries for the same value.

# The Creation Of The Index
To create the Starbucks Latte Index, we took a ten-step approach detailed in Google Colab Notebook. 

Let us dive right in!

# Setting Up The Notebook

First, we imported the necessary libraries to the Google Colab notebook.

Next, we wrote the functions that we needed when interpreting the data.

After this, we proceeded to extract and analyze data.

# 1. Scraping Starbucks latte prices
We scraped data taken from Cash Net USA using the "requests" library. Scraping the data allowed us to create a detailed "table" showing the prices of tall lattes in US dollars in 19 countries. However, our "table" was not formatted as a data science table. Instead, it was an array of divs. To fix the formatting issue, we used a loop to obtain the data from each div individually and put it into the rows and columns of a data science table.

# 2. Cleaning the latte prices data and converting prices from USD to CAD
After scraping the data into a data science table, we used a function to clean the latte price column. This function strips the dollar sign in the price column and converts all the strings to floats, enabling us to use these numbers in calculations. Once our data was clean, we used it for calculations and conversions. Since the prices we scrapped were in USD, we needed to convert them to CAD. To ensure the accuracy of the conversion, we utilized another predefined function that used an imported API from FXRatesAPI for the conversions. We then applied this function to the USD prices and saved the results in a new column.
Additionally, we calculated the Purchasing Power Parity by using the price in Canada as the base price for the index and dividing every other country's price by the Canadian price. We used a function to calculate the PPP and applied it to the USD prices, as the PPP index remains the same whether using CAD or USD. We saved the results in a new column for each country's index.

The resulting table is displayed in the picture below.

<table border="0" class="dataframe">
<thead>
<tr>
<th>country</th> <th>price of latte in USD</th> <th>price of latte in CAD</th> <th>Purchasing Power Parity</th>
</tr>
</thead>
<tbody>
<tr>
<td>Andorra       </td> <td>3.28                 </td> <td>4.61                 </td> <td>0.851948               </td>
</tr>
<tr>
<td>Argentina     </td> <td>4.67                 </td> <td>6.56                 </td> <td>1.21299                </td>
</tr>
<tr>
<td>Aruba         </td> <td>2.22                 </td> <td>3.12                 </td> <td>0.576623               </td>
</tr>
<tr>
<td>Australia     </td> <td>3.97                 </td> <td>5.58                 </td> <td>1.03117                </td>
</tr>
<tr>
<td>Austria       </td> <td>3.48                 </td> <td>4.89                 </td> <td>0.903896               </td>
</tr>
<tr>
<td>Azerbaijan    </td> <td>3.41                 </td> <td>4.79                 </td> <td>0.885714               </td>
</tr>
<tr>
<td>Bahamas       </td> <td>3.75                 </td> <td>5.27                 </td> <td>0.974026               </td>
</tr>
<tr>
<td>Bahrain       </td> <td>4.24                 </td> <td>5.95                 </td> <td>1.1013                 </td>
</tr>
<tr>
<td>Belgium       </td> <td>3.52                 </td> <td>4.94                 </td> <td>0.914286               </td>
</tr>
<tr>
<td>Bolivia       </td> <td>3.19                 </td> <td>4.48                 </td> <td>0.828571               </td>
</tr>
<tr>
<td>Brazil        </td> <td>1.96                 </td> <td>2.75                 </td> <td>0.509091               </td>
</tr>
<tr>
<td>Bulgaria      </td> <td>2.69                 </td> <td>3.78                 </td> <td>0.698701               </td>
</tr>
<tr>
<td>Cambodia      </td> <td>3.25                 </td> <td>4.56                 </td> <td>0.844156               </td>
</tr>
<tr>
<td>Canada        </td> <td>3.85                 </td> <td>5.41                 </td> <td>1                      </td>
</tr>
<tr>
<td>Chile         </td> <td>4.95                 </td> <td>6.95                 </td> <td>1.28571                </td>
</tr>
<tr>
<td>China         </td> <td>4.23                 </td> <td>5.94                 </td> <td>1.0987                 </td>
</tr>
<tr>
<td>Colombia      </td> <td>2.5                  </td> <td>3.51                 </td> <td>0.649351               </td>
</tr>
<tr>
<td>Costa Rica    </td> <td>4.22                 </td> <td>5.93                 </td> <td>1.0961                 </td>
</tr>
<tr>
<td>Cyprus        </td> <td>2.97                 </td> <td>4.17                 </td> <td>0.771429               </td>
</tr>
<tr>
<td>Czech Republic</td> <td>3.93                 </td> <td>5.52                 </td> <td>1.02078                </td>
</tr>
</tbody>
</table>

# 3. Factoring local tax rates into the calculation
The prices we scraped do not include the tax each Starbucks location would charge the consumers. Therefore, we wanted to examine if sales tax will affect PPP. Consequently, we scraped the sales tax in every country from Wikipedia; since the data was split into Euro and Non-Euro tables, we combined the two tables. Then, we needed to incorporate sales tax into the calculation, which sounded to us more straightforward than it was. It was more complicated than we thought because some countries have sales tax included in their price, and some do not; some countries have provinces, states, and cities that could charge different sales taxes within the same country. To tackle the tax challenge, we took the average sales tax that a consumer will pay in a country. For example, Brazil and Canada happened to have sales taxes that vary with location; therefore, we readjusted their sales tax accordingly. Using the tax data we gathered, we calculated a new PPP that includes sales tax and saved it in a new column. 

This resulted in the following table:

<table border="0" class="dataframe">
<thead>
<tr>
<th>Country</th> <th>Latte Price (USD)</th> <th>Latte Price (CAD)</th> <th>Purchasing Power Parity</th> <th>Sales Tax</th> <th>Purchasing Power Parity with tax</th>
</tr>
</thead>
<tbody>
<tr>
<td>ANDORRA       </td> <td>3.28             </td> <td>4.61             </td> <td>0.851948               </td> <td>0.045    </td> <td>0.852126                        </td>
</tr>
<tr>
<td>ARGENTINA     </td> <td>4.67             </td> <td>6.56             </td> <td>1.21299                </td> <td>0.21     </td> <td>1.21257                         </td>
</tr>
<tr>
<td>AUSTRALIA     </td> <td>3.97             </td> <td>5.58             </td> <td>1.03117                </td> <td>0.1      </td> <td>1.03142                         </td>
</tr>
<tr>
<td>AUSTRIA       </td> <td>3.48             </td> <td>4.89             </td> <td>0.903896               </td> <td>0.2      </td> <td>0.903882                        </td>
</tr>
<tr>
<td>AZERBAIJAN    </td> <td>3.41             </td> <td>4.79             </td> <td>0.885714               </td> <td>0.18     </td> <td>0.885397                        </td>
</tr>
<tr>
<td>BAHAMAS       </td> <td>3.75             </td> <td>5.27             </td> <td>0.974026               </td> <td>0.12     </td> <td>0.974122                        </td>
</tr>
<tr>
<td>BAHRAIN       </td> <td>4.24             </td> <td>5.95             </td> <td>1.1013                 </td> <td>0.1      </td> <td>1.09982                         </td>
</tr>
<tr>
<td>BELGIUM       </td> <td>3.52             </td> <td>4.94             </td> <td>0.914286               </td> <td>0.21     </td> <td>0.913124                        </td>
</tr>
<tr>
<td>BOLIVIA       </td> <td>3.19             </td> <td>4.48             </td> <td>0.828571               </td> <td>0.13     </td> <td>0.828096                        </td>
</tr>
<tr>
<td>BRAZIL        </td> <td>1.96             </td> <td>2.75             </td> <td>0.509091               </td> <td>0.22     </td> <td>0.508318                        </td>
</tr>
<tr>
<td>BULGARIA      </td> <td>2.69             </td> <td>3.78             </td> <td>0.698701               </td> <td>0.2      </td> <td>0.698706                        </td>
</tr>
<tr>
<td>CAMBODIA      </td> <td>3.25             </td> <td>4.56             </td> <td>0.844156               </td> <td>0.1      </td> <td>0.842884                        </td>
</tr>
<tr>
<td>CANADA        </td> <td>3.85             </td> <td>5.41             </td> <td>1                      </td> <td>0.109981 </td> <td>1                               </td>
</tr>
<tr>
<td>CHILE         </td> <td>4.95             </td> <td>6.95             </td> <td>1.28571                </td> <td>0.19     </td> <td>1.28466                         </td>
</tr>
<tr>
<td>CHINA         </td> <td>4.23             </td> <td>5.94             </td> <td>1.0987                 </td> <td>0.13     </td> <td>1.09797                         </td>
</tr>
<tr>
<td>COLOMBIA      </td> <td>2.5              </td> <td>3.51             </td> <td>0.649351               </td> <td>0.19     </td> <td>0.648799                        </td>
</tr>
<tr>
<td>COSTA RICA    </td> <td>4.22             </td> <td>5.93             </td> <td>1.0961                 </td> <td>0.13     </td> <td>1.09612                         </td>
</tr>
<tr>
<td>CYPRUS        </td> <td>2.97             </td> <td>4.17             </td> <td>0.771429               </td> <td>0.19     </td> <td>0.770795                        </td>
</tr>
<tr>
<td>CZECH REPUBLIC</td> <td>3.93             </td> <td>5.52             </td> <td>1.02078                </td> <td>0.21     </td> <td>1.02033                         </td>
</tr>
</tbody>
</table>

To validate our expectation that there will be little to no difference between the PPP without tax and the PPP with tax, we created a bar graph that displays both indexes for each country side by side.

<img alt="No description has been provided for this image" class="" src="data:image/png;base64,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UW7yWbrEYjGsra0xe/ZspVnQiIiIiOjjxgQSERERERERERGpxSLaRERERERERESkFhNIRERERERERESkFhNIRERERERERESkFhNIRKRVGRkZuHv3LjIyMrQdSpnBNtMc26xw2G6aY5tpjm1GRERUNjCBRERal52dre0Qyhy2mebYZoXDdtMc20xzbDMiIqLSjwkkIiIiIiIiIiJSiwkkIiIiIiIiIiJSiwkkIiIiIiIiIiJSiwkkIiIiIiIiIiJSiwkkIiIiIiIiIiJSiwkkIiIiIiIiIiJSS0/bARARERERkXZIpVKkp6cjIyND26EQEdEHpq+vj0qVKkFHp2B9i5hAIiIiIiL6BEmlUjx//hyGhoaoXr06RCKRtkMiIqIPRCaTISMjA8+fP0e1atUKlETiEDYiIiIiok9Qeno6DA0NYWBgwOQREdEnRiQSwcDAAIaGhkhPTy/QPkwgERERERF9gjIyMqCvr6/tMIiISIv09fULPIyZCSQiIiIiok8Uex4REX3aNPk9wAQSERERERERERGpxQQSERERERERERGpxQQSERERERERERGpxQQSERERERFRKRQREQGxWAxPT09thwIbGxvY2NhoOwwqJTw9PSEWixEREaHtUOgD0tN2AEREREREVPo8/e8FkpJTtR2GStWrVoG5qXGh93/w4AGaN2+usKxcuXIwNTVFhw4dMH36dFhbWxc1TCpBnp6e8PLyUlhWsWJF1K1bF3379sXUqVNRqVIlLUX3YURERKBv374KyypUqABzc3N06dIFM2bMQJ06dT5YPPLX1bBhw+Dt7f3BzksfDhNIRERERESkJCk5FYtW+2s7DJXmTXEtUgJJrl69ehg6dCgAID09HefOncOuXbtw8OBB7N+/H7a2tkU+x8fiwIED2g5BpX79+qFJkyYAgMTERBw6dAheXl4ICQnB4cOHUb58eS1HWPJatGiBnj17AgBevnyJyMhIbNu2DQcOHMDRo0fx2WefFfs5x48fj0GDBqF27drFfmwqvZhAIiIiIiKiT5KVlRXmzp2rsGzx4sVYtmwZFi1ahKCgIC1FVvrUq1dP2yGo9NVXX2HQoEHC94sWLUL37t1x6dIl7Ny5E25ublqM7sNo2bKlwn0sk8kwceJEBAYGYtmyZSXSG6hatWqoVq1asR+XSjfWQCIiIiIiIvp/48ePBwDExsYC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zQqH7aY5tpnm2Gba8+zZszxnpgKAp/+9QFJy6geMqOCqV60Cc1NjbYdBxWjbtm2YOnUqli9fjjFjxmg7HCphzs7OCAsLw/nz52FlZaXtcD55+f0+kGOqj4iIiIiIlJibGjNJQ8UuMTERpqamCrN7PX78GL///jt0dXXRs2dPLUZHH8L169cRFhaGrl27MnlUxjCBRFQC4m4/RHa2NP8NCVJpNl6/zsSbe4+go1P83aQ/RmwzzbHNCqck2o29BoiIPm0rV65EWFgYOnToABMTEyQkJCA0NBRpaWmYM2eOUjFr+njs3LkTt27dwvbt2wHk1OCisoUJJKISsHzjHqS9+nAzK5RlUmk23rzJgIGBPh/sC4htpjm2WeGURLvNm+LKBBIR0SfMwcEBN27cQFhYGFJSUqCvr4+mTZtizJgxGDJkiLbDoxK0ZcsWnD59GhYWFli9ejXat2+v7ZBIQ0wgERERERER0Qfh4OAABwcHbYdBWhAUFKTtEKiIOAsbERERERERERGpxQQSERERERERERGpxQQSERERERERERGpxQQSERERERERERGpxQQSERERERERERGpxQQSERERERERERGpxQTSR8TDwwNisRj16tVDZmamym2cnJwgFothZmaGhw8fqtymbdu2EIvFCssiIiIgFosV/tWqVQtNmzbF4MGDsXLlSjx58kRtfNnZ2fD19UX//v3x2WefwcTEBA0bNoSzszP279+f537vn7datWpo0KABnJ2dceLECZX7eHp6Ku1Xo0YNdOjQAYsWLUJqaqraWE+dOiXst2/fPrXbEhEREREREX3s9LQdABWPtLQ07Nu3DyKRCMnJyQgKCsLAgQPz3D4zMxOLFy/Ghg0bNDpPixYt0LNnTwDAmzdvkJiYiOjoaBw5cgReXl5YsGABJkyYoLTfs2fP4OrqipiYGJibm8PR0REmJiZ49OgRwsLCEBoail69emHTpk2oVKmS0v7GxsYYN26cEHtcXJyw38aNGzF48GCV8fbr1w9NmjQRYggLC8Py5csREhKCY8eOoUKFCir3k0gkAACRSCQkvYiIiIiIiIg+VUwgfST27t2L9PR0eHh4wNvbGxKJRG0CqV69eti1axemTp0Ka2vrAp+nZcuWmDt3rtLyoKAgTJkyBbNnz0bFihXh7u4urHv79i3c3NwQExMDd3d3LF26FAYGBsL6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ZUZGRgaWLVuGa9eu4dChQzA3N8fAgQO1HRYRERERERHRR489kKjMyMjIwPLly3H69Gn06dMHQUFBMDIy0nZYRERERERERB899kCiMkMsFiM5OVnbYRARERERERF9ctgDiYiIiIiIiIiI1GICiYiIiIiIiIiI1OIQNqISkFHNHSJItR1GmSDNzsabN68hMqgIHV1dbYdTJrDNNMc2K5zS0m4yXbHWzk1EREREOZhAIioBMn0ryLQdRBmRkZGBR8nxsDC0gL6+vrbDKRPYZppjmxUO242IiIiI5DiEjYiIiIiIiIiI1GICiYiIiIiIiIiI1GICiYiIiIiIiIiI1GICiYiIiIiIiIiI1GICiYiIiIiIiIiI1OIsbEQlIO72Q2RnS7UdRpkglWbj9etMvLn3CDo6nF69INhmmmObFQ7bTVH1qlVgbmqs7TCIiIiItIIJJKISsHzjHqS9eq3tMMoEqTQbb95kwMBAnw+oBcQ20xzbrHDYbormTXFlAomIiIg+WRzCRkREREREREREajGBREREREREREREajGBRERERERERERE/8fevcdFWeb/H3/PDHLSdCQFQzEhczusZZalltpmrueyTEHU0tosNy396q6HLA9ZaHmo1Wy/33QzGYRUPGaZqXlEzbLssG1q4NmwQDzBQMw9vz9a5hcBAwPoMPB6Ph48jLmv+74+92fbR/D2vq7bLQIkAAAAAAAAuEWABAAAAAAAALcIkAAAAAAAAOAWARIAAAAAAADcIkDycUePHpXVai3yFR4ervbt22vGjBm6ePFiiefv2rXLdc7q1atLHJeQkCCr1aq5c+eWOCYuLk5Wq1XJyckljklMTHTNt3///lKvZbVaNWnSpBLHTZ482TUuLi6uxHFlvU9JOn78uMaMGaPWrVsrLCxMjRs31i233KL+/fvr9ddf16VLl9yeDwAAAABAdePn7QJQOSIjI9W/f39JktPpVEZGhj7++GPNmDFDmzdv1oYNG2SxWIqcFx8fL0kymUyy2Wzq06fPZa0zPj5eJpNJTqdTNptNrVu3djvez89Py5Yt05QpU+TnV/hf1/z8fCUlJcnPz0/5+fmlziuVfp9ff/21evXqpXPnzqlt27a6//77VadOHZ04cUIpKSnauHGjHnjgAUVFRZX9pgEAAAAA8HEESNVEVFSUJkyYUOiz3NxcdenSRfv27dPO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CggIUIcOHSRJmZmZRY4nJycrOztbMTExiomJkWEYWrp06RWrr23btmrRooVycnL0/fffFzsmPj5efn5+eu6559ShQwdt27ZNx44d83iu66+/XtHR0friiy+0atWqipYOAAAAAEC1QIAE5eXlaefOnTKZTGrZsmWR4/Hx8bJYLOrfv7969+6tOnXqKCEhQU6n84rXWtzyuv/85z/at2+f7rvvPoWGhrpCroSEhHLNMXHiRAUEBGj69On65ZdfKloyAAAAAAA+jyVsNUxqaqri4uIk/boHUmZmpjZv3qzTp09r2rRpat68eaHx3377rfbv36/OnTsrLCxMktSrVy8lJSVp+/btJe4TtHXrVtnt9mKP7dy506Oa9+zZo4MHDyokJEQtWrQocrxgf6bo6GhJUu/evTV27FglJCRo3LhxMps9y0kjIiI0bNgwzZs3T++8846GDRvm0fmS5DQcMgyHx+fVRIZhFPoTpaNnnqNn5UPfPFfVe2YYjhL/++wteXl5hf6sjgIDA71dAgAAFUaAVMOkpaVp5syZRT7v2rVrsWFQQTgTExPj+mzAgAFKSkpSfHx8iQHStm3btG3bNo/ry8/PdwVcv91E22w2a/bs2UV+APvll1/03nvvqW7duurZs6ckqU6dOurZs6eWLVumrVu36r777vO4jjFjxmjJkiV67bXXFBsbqzp16nh0/pwx98tp5Hs8LwAAl5Nhcer48ePeLqNYv307anVisVgUFRXl7TIAAKgwAqQapnPnzkpOTnZ9n5mZqT179mj8+PHq1q2b1q5dqzvuuEPSr5trL1u2TFdddZV69erlOqdDhw5q0qSJ3n//fWVlZclqtRaZZ/LkyRo9enSxNcTFxRUbYkmSw+EocszPz0+LFy8uVEOBDz74QD///LMGDx5cKFwaMGCAli1bpvj4+HIFSFarVaNHj9aUKVM0b968Iht7lyY0d6VMxiWP562JDKeh3NxcBQQEyGxiVW1Z0DPP0bPyoW+eq+o9szd8UsF1r/V2GYXk5eUpPT1dYWFh8vf393Y5AACgBARINVxISIh69Oih4OBg9enTR9OnT9fq1aslSevXr1dmZqYGDhyooKAg1zlms1n9+vXT3LlztXz5cj355JOVVk9AQIDrbyAvXryo7du3a8SIEXr66af14YcfFtmjqbgnpCSpU6dOCg8P1wcffKCzZ8+q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fTMMh+x2u9fmz8vLK/QnSlcTesZfQgEAqgMCpBokLS2t2CVhXbt2LbL3UYH58+cX+3ndunXLFSAVPN1zzTXXFHu8uA2zf79v0+XSqlUr3XzzzUpISHAFSAkJCfrjH/+oVq1aeRQgzRlzv5wGG24DwJWU46itrGzp+PHj3i5F6enp3i7B51TXnlksFkVFRXm7DAAAKowAqQbp3LmzkpOTXd9nZmZqz549Gj9+vLp166a1a9fqjjvuKHTO999/X+mbaLtTXMB1pQIkSRo0aJAmTJigTz/9VNKv9z9jxgyPrxOau1Im41Jll1ctGU5Dubm5CggIkNnEqtqyoGeeo2fl42t9szd8UvUbNPZqDXl5eUpPT1dYWJj8/f29WouvoGcAAPgGAqQaLCQkRD169FBwcLD69Omj6dOna/Xq1Zd1zoYNG0qSTp8+XezxrKws1z+3adNGhw4dKtN1TSaTnE5niccLll+Yze5/AYqOjtbkyZNdm2n7+/urf//+Zarht8wWs0w+8MtWlfDflX5mk1lmCz0rE3rmOXpWPj7WN7PFUmWWCvn7+1eZWnwFPQMAoGojQIJuv/12SdL+/fsv+1y33XabatWqpQMHDujChQuVtg9S3bp1dfbsWTmdTplMpiLHMzIyXOPcKQjVVq1aJUnq2bOnQkJCKqVGAAAAAAB8VdX/60RcdgVP/bh7gqey1K5dWw899JCys7O1YMGCSrvuTTfdpEuXLunbb78t9njBkrSbb7651GsNGjRIFy5c0IULFzRo0KBKqxEAAAAAAF9FgAS9+eabkqT27dtfkflefPFFNWjQQK+++qreeustORxF31Zmt9uVm5tb5msOGDBAkjR58uQi52VlZbk25y4Y5859992nhIQEJSQk6E9/+lOZawAAAAAAoLpiCVsNkpqaWugtZ2fPntXevXt14MABWa1WTZkypcg58+bNU+3atYu93v333682bdoU+mzRokXatGlTseMfffRRtWvXTk2aNNGqVatcG1bPnz9fHTp0UHh4uHJycnT69Gl98sknOnfunNq1a1emexs0aJA2btyo999/X7fffrv+/Oc/KyQkROnp6frggw+UkZGhp59+usS3zf2W2WxWz549yzQvAAAAAAA1AQFSDZKWllboLWcBAQEKDw/XE088oVGjRikiIqLIOfPnzy/xevXq1SsSIKWkpCglJaXY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VeWeNahfV41CQ7xdBgAAAOBWhQKkAwcOaMyYMXI4HGrXrp1Gjhypm266SY0aNdKPP/6of//735o3b552796t//mf/9Gtt96qW2+9tbJqB6qs2QtX6sLFbG+X4RMMw6GcHLuCggKr3C/2VRU981xV7tkLI2MJkAAAAFDlVWgT7fnz58vhcGjEiBH64IMP1L17d1177bUKCAjQtddeq+7du+uDDz7QyJEj5XA49Oabb1ZW3QAAAAAAALhCKhQgpaSkqF69enrxxRfdjnvhhRdUt25d7dq1qyLTAQAAAAAAwAsqFCD99NNPuu6661SrVi2342rVqqXmzZvr559/rsh0AAAAAAAA8IIKBUh16tRRenp6mcamp6erdu3aFZkOAAAAAAAAXlChAOmWW27RqVOn9MEHH7gdt379ep08eVK33HJLRaYDAAAAAACAF1QoQBo0aJCcTqeGDRum+fPnKzu78FunsrOzNW/ePD311FMymUwaPHhwhYoFAAAAAADAledXkZMfeeQRrVu3TmvXrtWLL76oV155RU2bNlVoaKjOnDmjY8eOyW63y+l06sEHH1Tfvn0rq24AAAAAAABcIRV6AkmS/vWvf2ncuHGqU6eOcnJy9P3332vHjh36/vvvlZOTozp16mj8+PFatGhRZdSL/zp69KisVmuRr/DwcLVv314zZszQxYsXC53TsmVLWa1Wt9ctbkxCQoKsVqvmzp1b5vry8/P13nvvacCAAbrxxhsVGhqq8PBw3X777Ro2bJjWrVsnwzBKPN/pdOq2226T1WpV//793c71+x5cffXVuv766xUdHa2tW7cWe05cXJysVquSk5NLvG5iYqLrmvv37y/TfQMAAAAAUB1V6AkkSbJYLBo/fryeffZZ7d69W4cOHdLFixdVp04dtWjRQm3btlVwcHBl1IpiREZGugIWp9OpjIwMffzxx5oxY4Y2b96sDRs2yGKxXNGajh07pkGDBumrr77S1VdfrU6dOikiIkKGYejo0aPatGmTli1bpp49eyohIaHYa+zYsUNpaWkymUzavHmzTp8+rWuuuabEOUNCQvTkk09KknJzc/Xdd99p48aN+uijj7Rw4UI98sgjHt9HfHy8TCaTnE6nbDabWrdu7fE1AAAAAACoDiocIBUIDg5W586d1blz58q6JMogKipKEyZMKPRZbm6uunTpon379mnn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AACAWwRIAAAAAAAAcIsACQAAAAAAAG4RIAEAAAAAAMAtAiQAAAAAAAC4xVvYgMvgu8PH5HAY3i7DJxiGQ9nZucpJOymzuWq9Xr2qomeeo2flU1l9a1C/rhqFhlRiZQAAALjSCJCAy2D2wpW6cDHb22X4BMNwKCfHrqCgQH6xLyN65jl6Vj6V1bcXRsYSIAEAAPg4lrABAAAAAADALQIkAAAAAAAAuEWABAAAAAAAALcIkAAAAAAAAOAWARIAAAAAAADcIkACAAAAAACAWwRIAAAAAAAAcIsAyUd8+eWXGjFihFq3bq3w8HA1atRIrVq10rBhw/TJJ58Ue86lS5cUEREhq9WqsWPHlnjto0ePymq1ymq1qkWLFsrPzy923Pfff+8a17Jly0LHEhISXMcKvurXr6+mTZuqe/fustlsJc7vcDhks9nUp08fXXfddWrYsKFatGih6OhorVmzpsTzfj9fo0aN1KJFC3Xr1k2TJk3S119/7fZ++/btW+K1y9o7AAAAAABqAj9vFwD3DMPQpEmTtGDBAvn5+aljx47q3r27atWqpSNHjmjjxo1atmyZJk6cqL///e+Fzl21apUuXLggk8mk5cuXa/r06QoMDCxxLj8/P505c0YbN25Ujx49ihyPj4+X2ew+c+zUqZPatm0r6ddg6MSJE/rggw80YsQIff/993rppZcKjf/pp58UGxurffv2qVGjRurRo4caNmyokydPauPGjfroo4/UrVs3LVq0SLVr1y4yX0hIiJ588klJUn5+vjIyMvTVV19p/vz5mj9/vgYNGqTZs2crICDAbd2/52nvAAAAAACozgiQqrjp06drwYIFatmypZYsWaLIyMhCx3NycvT2228rMzOzyLk2m01+fn568skn9dZbb2ndunXq169fiXPdeeed+uabb2Sz2YoESPn5+Vq2bJnuvfde7dq1q8Rr3HvvvRo9enShz44ePar27dvr//7v/zRx4kQFBQVJkn755RcNHDhQ+/bt0+DBg/Xqq6+6jklSVlaWnnrqKW3YsEHPPPOMFi9eXGS+q6++WhMmTCjy+b///W899dRTstlsysvL0//93/+VWHNxPO0dAAAAAADVGUvYqrDU1FS98cYbCgkJUXJycpHwSJKCgoL07LPPFglRDh06pD179qhz587661//KpPJpPj4eLfzBQUFqW/fvtq4caN++umnQsc2bNigM2fOaNCgQR7fx7XXXqvmzZsrNzdXFy9edH2emJioTz/9VO3atdM//vGPQuGR9OsStcWLFysqKkqrV6/Wtm3byjznTTfdpFWrVqlBgwZatmyZPv/88zKfW57eAQAAAABQnREgVWFLly6Vw+HQ0KFDFRoa6nbs75doFQQeAwYMUEREhO655x7t2LFDR44ccXudQYMGKT8/X0lJSYU+t9lsql+/vnr27OnxfRw7dkyHDx9W48aN1bBhQ9fnCQkJkqSxY8fKZDIVe25QUJBGjBhRaHxZNWjQQEOHDpUkrVy5ssznlbd3AAAAAABUVyxhq8L27NkjSerYsaNH5xUEQPXq1VO3bt0kSdHR0dqxY4dsNpsmTZpU4rm33367brrpJi1dulQjR46UJKWnp2vTpk16/PHHS91LaOvWrbLb7ZJ+3QPp5MmT+vDDDxUcHKwFCxYUqnH//v3y8/PT3Xff7faanTp1kiR9+umnpd/879xzzz167bXXtH///jKNr0jvfstpOGQYDo/rrYkMwyj0J0pHzzxHz8qnsvpmGA7Xfxuqu7y8vEJ/onQ1oWfsowgAqA4IkKqwM2fOSJLCw8M9Oq9gudljjz3m+oHlwQcf1N///nclJiZq4sSJbjfDHjhwoJ5//nl99tlnuuOOO5SYmKj8/PwyLV/btm1bkaVmfn5+Gjp0qG666SbXZ5mZmfrll18UFhZW6g9VjRs3lvRrkOWpa665xjVfWVS0dwXmjLlfTqP4t9kBQE2S46itrGzp+PHj3i7liirPf7NquuraM4vFoqioKG+XAQBAhREgVUMFS7BiYmJcn1111VXq2bOnli9frs2bN6tLly4lnh8dHa0pU6bIZrPpjjvuUEJCgm655Rbdcsstpc49efJk1ybahmHoxx9/1Pr16zVp0iR9/PHH2rZtm+rVq1fBO7x8Ktq7AqG5K2UyLl22OqsTw2koNzdXAQEBMptYVVsW9Mxz9Kx8KqNv9oZPqn6DxpVcWdWVl5en9PR0hYWFyd/f39vl+AR6BgCAbyBAqsJCQ0N18OBBnTp1Stdff32Zzjl9+rQ2bdqkZs2aqV27doWOxcTEaPny5bLZbG5DkAYNGqhbt25auXKl+vTpo0OHDunVV1/1uH6z2azw8HA9+eSTSk9P16xZs/T2229r7NixCgkJUa1atZSRkSG73e72KaSTJ09KksLCwjyu4fTp05J+fVtbWcZWtHcFzBazTPySWjb/XelnNpllttCzMqFnnqNn5VMJfTNbLDVy+Y6/v3+NvO+KoGcAAFRt/BRdhbVt21aStH379jKfU7Dx9pEjR2S1Wgt99e3bV5L04YcfKiMjw+11Bg8erPPnz+uvf/2rAgMD1b9///LfiH7dW0mSay8iPz8/tW7dWvn5+dq1a5fbcwuWxN15550ez7tz505JUuvWrUsdW1m9AwAAAACguuEJpCosNjZWc+fO1eLFizV8+HA1aNCgxLG5ubny9/eXzWZznWuxWIqMO3jwoPbu3aukpCQ988wzJV6vc+fOCg8P16lTp9S3b19ZrdYK3UtWVpakwhuxxsbGau/evZozZ47uu+++Yt/EZrfb9eabb0r6dW8mT/z8889avHixJLkCoJI4nc5K6x0AAAAAANUNAVIVFhUVpeeee05z5szRI488osWLF6tZs2aFxtjtdi1cuFAZGRm67777lJaWpvbt2xd649lvHTp0SG3atJHNZnMbglgsFiUkJOjkyZNq2bJlhe7Dbrdr0aJFklTojWuxsbGKj4/Xrl27NHr0aM2YMaPQo+vnzp3T008/rR9++EF9+vRxvY2tLL777jsNGzZMP/30kwYMGKDbbrvN7fidO3dWWu8AAAAAAKhuCJCquEmTJslut2vBggVq06aNOnbsqBtvvFG1atXS0aNHtXXrVmVmZmrSpEmuDaDdPalz/fXX66677tLevXtdb1kryW233VZq8PJ7W7dudb2q2TAMnTlzRps2bXIFUU888YRrbK1atbR06VINGDBAixcv1kcffaQuXbqoYcOGOnXqlD766CNlZmaqa9eurqeQfi8jI0NxcXGSJIfDoczMTB04cECff/65JOnRRx/VrFmzSq27snsHAAAAAEB1QoBUxZnNZr3yyivq16+fFi1apJSUFKWkpMgwDIWFhalz584aOHCgbrvtNt1www2qXbu2HnzwQbfXHDhwoPbu3av4+PhKD0G2bdvm2rNIkmrXrq2oqCgNHTpUf/3rXxUcHFxofGhoqD766CMtXbpUK1as0Pvvv68LFy7IarWqTZs2io2NdXs/mZmZmjlzpiQpICBAdevW1XXXXaeRI0cqOjpaf/zjH0ut+dy5c1q3bp3XewcAAAAAQFVlysrKcnq7CKC6CTo5VSbjkrfL8AmG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BgAAAAAAALcIkAAAAAAAAOAWARIAAAAAAADcIkACAAAAAACAWwRIAAAAAAAAcIsACQAAAAAAAG4RIAEAAAAAAMAtAiQf8+WXX2rEiBFq3bq1wsPD1ahRI7Vq1UrDhg3TJ598UmS83W7XW2+9pe7duysyMlKhoaG66aabNGTIEG3btq3YOY4ePSqr1aq+ffuWua4DBw7or3/9q2699VY1atRITZs21b333quZM2fq3LlzxZ4zfPhwWa1WWa1W/d///V+J1x46dKhrXEJCQqFjLVu2dB0r+AoNDdUtt9yi5557TkePHi1yvbi4OFmtViUnJ5c4Z2Jiout6+/fvL2MXAAAAAAConvy8XQDKxjAMTZo0SQsWLJCfn586duyo7t27q1atWjpy5Ig2btyoZcuWaeLEifr73/8uSUpNTVX//v11+PBhNWvWTA899JDq1avnGr969WoNGTJEs2bNkp9f+f9VmDlzpmbMmCE/Pz/dd999euihh5STk6OdO3cqLi5O//rXv5SYmKjWrVsXe76fn59sNpuGDRtW5NjZs2f1wQcfyM/PT/n5+cWeb7FYNHbsWNf3586d0+eff653331X69at07Zt2xQREeHRPcXHx8tkMsnpdMpms5VYOwAAAAAANQEBko+YPn26FixYoJYtW2rJkiWKjIwsdDwnJ0dvv/22MjMzJf0aovTt21dpaWn629/+pvHjx8tisbjGnz59WgMHDtTixYtVt25dTZs2rVx1vf3224qLi1OzZs20bNkytWjRotDxd955R2PHjtUjjzyi7du3q0mTJkWucf/992vDhg36+uuv1bJly0LH3nvvPeXm5qp79+768MMPi63Bz89PEyZMKPL52LFjtXDhQi1ZskTPP/98me/phx9+UEpKirp3765Dhw5pxYoVevnllxUUFFTmawAAAAAAUJ2whM0HpKam6o033lBISIiSk5OLhEeSFBQUpGeffdYVpMybN09paWnq37+/nn/++ULhkSRdc801SkpKUv369TV//nylpqZ6XFdWVpamTZsmf39/JSUlFQmPpF+Xn40aNUqZmZl66aWXir3OgAEDZLFYFB8fX+RYQkKC/vCHP+jOO+/0uL7OnTtLkitUKyubzSZJiomJUXR0tM6fP681a9Z4PD8AAAAAANUFAZIPWLp0qRwOh4YOHarQ0FC3YwMCAiTJtVfQ3/72txLHhoaG6rHHHpNhGFq6dKnHda1Zs0YXLlxQ7969dcMNN5Q4buTIkQoMDNTKlSuVnZ1d5Hh4eLjuu+8+rVixQnl5ea7Pv/zyS3399dcaOHCgx7VJ0pYtWyRJt956a5nPcTgcrv2PunXrpujoaJlMpmLDLQAAAAAAagqWsPmAPXv2SJI6duxYpvHHjh3T6dOnFR4eruuvv97t2E6dOun111/Xp59+6nFde/fudV3DHavVqltvvVV79+7Vl19+qfbt2xcZM2jQIH388cf64IMP1KdPH0m/Pgnk5+enmJiYIptn/1Z+fr7i4uJc31+4cEH79+/Xp59+qocfflgxMTFlvqeNGzfqxx9/1NChQxUQEKCmTZuqXbt2SklJUWpqqqKiosp0HafhkGE4yjxvTWYYRqE/UTp65rnK7plhOGS32yvlWlVZQaj/23Af7tEzz9WEngUGBnq7BAAAKowAyQecOXNG0q9P6ngyvnHjxqWOLRiTnp5e7roqY54ePXro6quvls1mU58+fWS327VixQr9+c9/LvWpK4fDoZkzZxb5/KabbtJDDz0kf3//UusrUPCk0W9Dp5iYGKWkpMhms+nFF18s03XmjLlfTqP4Tb8B+D7D4tTx48e9XcYVU57/RtR09Mxz1bVnFoulzH8BBQBAVUaAhCqhVq1a6t+/v/73f/9Xp06dUkpKirKysjRo0KBSzw0ICCj0Q+fFixf1n//8R1OnTtXgwYM1c+ZMPfXUU6VeJz09XRs3blRUVJTuuusu1+d9+vTRuHHjlJiYWOx+UsUJzV0pk3Gp1HGQDKeh3NxcBQQEyGxiVW1Z0DPPVXbP7A2fVHDdayuhsqotLy9P6enpCgsL8yiMr8nomefoGQAAvoEAyQeEhobq4MGDOnXqVKlL0grGS9LJkydLHVswJiwsrFx1VeY8gwYN0ltvvaWlS5dq586dCgsL05///GeP66pTp47uuOMOxcfH6+abb9bLL7+swYMHKzg42O15iYmJys/PV3R0dKHP69atqx49eig5OVmbNm1S165dS63BbDHLxC/2ZfPflX5mk1lmCz0rE3rmuUrumdliqVFLUvz9/WvU/VYGeuY5egYAQNXGbx4+oG3btpKk7du3l2l806ZNdc011+jUqVM6dOiQ27Hbtm2TpHK95azgKZ2Ca5QkKytLBw4ckL+/v1q1alXiuJtvvlmtW7fWwoULtX37dsXExMjPr/wZp9VqVfPmzXX+/HkdPny41PEFb1+Li4uT1Wot9JWcnCxJbKYNAAAAAKiRCJB8QGxsrCwWixYvXqyff/7Z7djc3FzXOZI0a9asEsf+9NNPWrJkicxms2u8Jx588EHVqVNH69at08GDB0scN3/+fNntdj300EOlPgU0aNAg/fjjjzIMo0zL10qTlZUlqfSNc1NSUnT48GFFRkZq8ODBxX41aNBAH330kX766acK1wUAAAAAgC8hQPIBUVFReu6555SRkaFHHnlER44cKTLGbrdr/vz5mjFjhiRp5MiRuvbaa/Xee+9p5syZcjgKvxEsPT1dsbGxyszM1IgRI8q1uaPVatWkSZOUl5enmJiYYp/yWbJkiebOnauQkBC98MILpV6zf//+stlsWrFiRZmW67mzbt06HT16VFarVTfddJPbsQVPFo0ZM0bz5s0r9uvRRx/VL7/8oqSkpArVBQAAAACAr2EPJB8xadIk2e12LViwQG3atFHHjh114403qlatWjp69Ki2bt2qzMxMTZo0SZJcy6769++vuLg4JSUlqXPnzqpbt66OHDmijRs36uLFi3rsscdKfLPYv//9bw0fPrzYYy1atNDo0aP19NNPKyMjQ6+99prat2+vzp076w9/+IPsdrt27typb775RqGhoUpMTFSTJk1Kvc86deqoV69eHvUmPz9fcXFxru+zs7P1n//8R5s2bZLJZNKrr77qdlPO8+fPa82aNapdu7b69OlT4rjY2FjNmTNH8fHxGjlypEc1AgAAAADgywiQfITZbNYrr7yifv36adGiRUpJSVFKSooMw1BYWJg6d+6sgQMH6t5773Wd07x5c+3atUv/+te/tHbtWi1fvlzZ2dlq0KCBOnfurMcff1ydOnUqcc7Tp08rMTGx2GN33323Ro8eLUl6/vnn1bNnT/3zn//Url27tGXLFvn7+ysyMlLjx4/X008/LavVWpntKMThcGjmzJmu7/38/NSgQQP17t1bzzzzTKE3qhVn5cqVys7O1oABA1SnTp0SxzVv3lxt27bVnj17tHfv3lKvCwAAAABAdWHKyspyersIoLoJOjlVJuOSt8vwCYbDUI49R0GBQbxRrIzomecqu2f2hsNkBDavhMqqNrvdruPHjysiIoK3Y5URPfMcPQMAwDfwmwcAAAAAAADcIkAC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69evqygqeQKBAF9//TUEAgGWL18uN6+Jo6MjcnNzcePGDYXHX7p0CQDg5ORU6nPWrVu3/AETERERERER1WAsIJEMOzs7zJo1C5mZmfj000+Rmpoq1yY/Px/ff/89vv7666oP8C1t27aFj48PkpKScPDgQZl9n332GYA3Q99KFrqys7OlE3hL2gFAbm4u1qxZI3066W1FRUXYsGEDgDdPaRERERERERG9TziEjeQsWrQI+fn5CA4OhqurKzw8PODg4ABdXV3cu3cPMTExyMrKwqJFizQdKubPn4/jx4/jm2++waeffgodnTe39OjRoxEZGYljx46hY8eO6N27N0xMTJCeno4TJ04gMzMTX3zxhcwwvcLCQqxcuRJff/01XF1d0aZNGxgbG+PJkyeIjo7GP//8g2bNmklXZyMiIiIiIiJ6X7CARHK0tLSwatUqDB06FCEhIbhw4QIuXLgAsVgMS0tLeHt7Y9SoUejRo4emQ4WzszP69++P8PBw7Nu3D2PGjAHw5hpCQ0OxZ88e7N+/H4cOHUJubi7q16+P9u3bY+zYsRgwYIBMX8bGxvjxxx9x+vRpxMfH4+jRo8jKykKdOnXQvHlz+Pr64osvvkD9+vU1calEREREREREGiPIzs5WvlQVEZWL4T/LuApbKYlFYuTl58HQwPC9n9y4tJizsmPO/pVvPhligxala5ufj7S0NDRt2pSTG5cSc1Z2zBkREVHN8H7/Fk1ERERERERERO/EAhIREREREREREanEAhIREREREREREanEAhIREREREREREanEAhIREREREREREanEAhIREREREREREamko+kAiGqjfNMxEECs6TBqBLFIhLy8VxAY1oGWtramw6kRmLOyY87+Vawt1HQIRERERFQDsYBEVAmKDexQrOkgaoj8/Hz88ywNTes2hYGBgabDqRGYs7JjzoiIiIiIKoZD2IiIiIiIiIiISCUWkIiIiIiIiIiISCUWkIiIiIiIiIiISCUWkIiIiIiIiIiISCUWkIiIiIiIiIiISCUWkIiIiIiIiIiISCUdTQdAVBv9fec+RCKxpsOoEcRiEV69eo28lH+gpaWt6XBqBOas7Jiz8mHeyq40OTNrYIyGFiZVHBkRERFRxbCARFQJvt1+GC9evtJ0GDWCWCxCXl4+DA0N+AG1lJizsmPOyod5K7vS5GzxzJEsIBEREVGNwyFsRERERERERESkEgtIRERERERERESkEgtIRERERERERESkEgtIRERERERERESkEgtIRERERERERESkEgtIRERERERERESkUo0qIF29ehUzZsxAhw4dYGVlhYYNG6J9+/aYPHkyzpw5I2137tw5CIXCUn05OztLj7t3716Z2r/t4cOHWLZsGTw8PGBtbQ1zc3O0atUKw4YNQ1hYGAoKCuTimz17ttJrDQsLg1AoxNq1a0uVm8DAQLlYGzVqhK5du2LFihXIyclReFxpcvQ2Hx8fmX0NGjRAs2bN0LdvX4SFhaG4uFjuOqdOnao0bmVtSp5HKBTCzMwMTk5OmDhxIm7cuFGhnEnydejQIYX7y/J6EhEREREREdV2OpoOoDTEYjEWLVqE4OBg6OjowMPDA3379oWuri5SU1MRGRmJgwcPYsGCBZg3bx6sra0xf/58lX0ePHgQKSkpcHBwkNtna2uLYcOGKTyufv36ctt++uknzJw5E3l5eWjfvj2GDx8OY2NjpKenIzY2FpGRkThw4ADCw8PLl4AyGDBggPSanj59isjISHz77beIiIhAdHQ09PX15Y4xMTHBpEmTynSeGTNmwMjICCKRCPfu3cMvv/yCixcv4urVq1i9erVaruXt8wBAbm4url+/jkOHDuH48eM4ceIEXFxc1HYuier0ehIRERERERFVBzWigLRy5UoEBwfD2dkZoaGhsLW1ldmfl5eHbdu2ISsrCwDQrFkzBAQEKO3v6NGjSElJQdOmTfG///1Pbr+dnZ3K49926tQpTJ48GfXr18fevXvx4YcfyuwvLi7GsWPH8MMPP5Sqv4oaOHAghgwZIv0+Pz8fPXv2xF9//YUff/wRo0ePljvG1NS01NcrMXPmTFhaWkq/v3HjBnr27Int27dj+vTpsLGxKfc1qDoPAGzYsAFLlizB5s2bsWXLFrWcR6K6vZ5ERERERERE1UG1H8J29+5drF+/HiYmJjh06JBc8QgADA0N4efnV6oiyI0bNzBt2jQYGhpiz549MDU1LXdsIpEIc+bMgVgsxq5du+SKDQAgEAjQv39/jRUcDAwMpE9TXbt2rdLO4+TkhG7duqG4uBhXr16ttPMAgLe3NwBIC4bqUhNeTyIiIiIiIiJNqPZPIO3duxcikQjjx4+HhYWFyraKhme97dmzZxg1ahRyc3Oxbds2tGvX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xt8GiYiIiIiIiIhIJRaQiIiIiIiIiIhIJRaQiIiIiIiIiIhIJRaQiIiIiIiIiIhIJRaQiIiIiIiIiIhIJRaQiIiIiIiIiIhIJRaQiIiIiIiIiIhIJR1NB0BUG+WbjoEAYk2HUSOIRSLk5b2CwLAOtLS1NR1OjcCclR1zVj7MW9mVJmfF2sKqDYqIiIhIDVhAIqoExQZ2KNZ0EDVEfn4+/nmWhqZ1m8LAwEDT4dQIzFnZMWflw7yVHXNGREREtRWHsBERERERERERkUosIBERERERERERkUosIBERERERERERkUosIBERERERERERkUosIBERERERERERkUosIBERERERERERkUosIBERERERERERkUosIBERERERERERkUosIBERERERERERkUosIBERERERERERkUosIBERERERERERkUosIBERERERERERkUosIBERERERERERkUosIBERERERERERkUosIBERERERERERkUosIBERERERERERkUosIBERERERERERkUosIBERERERERERkUosIBERERERERERkUosIBERERERERERkUosIBERERERERERkUosIBERERERERERkUosIBERERERERERkUosIBERERERERERkUosIBERERERERERkUosIBERERERERERkUosIBERERERERERkUosIBERERERERERkUosIBERERERERERkUosIBERERERERERkUosIBGRxmlra2s6hBqHOSs75qx8mLeyY87KjjkjIiKq/gTZ2dnFmg6CiIiIiIiIiIiqLz6BREREREREREREKrGAREREREREREREKrGAREREREREREREKrGAREREREREREREKrGAREREREREREREKrGAREREREREREREKrGAREREREREREREKrGARKTClStXMHToUFhbW8PKygo9e/bEzz//XKY+Xr9+jaCgIHTo0AGWlpZo3bo1Zs2ahadPn1ZS1JpVkZwVFxcjKioK/v7+cHNzg7W1NRo1aoRu3brh22+/RX5+fiVHrznquNfelp2dDQcHBwiFQgwZMkSNkVYf6srZ06dPERAQIH2P2traolevXggJCamEqDVLHTl79OgR5s+fj86dO8PKygr29vb46KOPsH//fohEokqKXHMOHDiA//znP+jRowcsLCwgFAoRFhZW5n7EYjG2bNkCNzc3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
"/>

As we can see above, our expectation that sales tax does not change the PPP Index significantly was right.

# 4. Displaying the currencies for each country and showing the price differences

Our next objective is to display each country's currencies by symbol and code. To achieve this, we imported a CSV file that contains information about country names and their respective codes. We then selected specific columns from the imported file, relabeled column names for clarity, and joined them with our latte table to get the currency code column. After that, an essential step in our process was using a function that gave us the exchange rates for every currency code. We saved the exchange rates into an array variable so we could use it to multiply each price and get a local currency for every country. Next, we wanted to know the difference between the latte prices in Canada and other countries. Therefore, we subtracted the price of a Canadian latte from that of a converted to CAD foreign latte.

Below is the table that we have created.

<table border="0" class="dataframe">
<thead>
<tr>
<th>Country</th> <th>Currency</th> <th>Currency Code</th> <th>Latte Price in Local Currency</th> <th>Latte Price (CAD)</th> <th>Sales Tax</th> <th>Price Difference (CAD)</th> <th>Purchasing Power Parity</th> <th>Purchasing Power Parity With Tax</th>
</tr>
</thead>
<tbody>
<tr>
<td>ANDORRA       </td> <td>Euro             </td> <td>EUR          </td> <td>3.13                         </td> <td>4.61             </td> <td>0.045    </td> <td>-0.8                  </td> <td>0.851948               </td> <td>0.852126                        </td>
</tr>
<tr>
<td>ARGENTINA     </td> <td>Argentine Peso   </td> <td>ARS          </td> <td>4719.38                      </td> <td>6.56             </td> <td>0.21     </td> <td>1.15                  </td> <td>1.21299                </td> <td>1.21257                         </td>
</tr>
<tr>
<td>AUSTRALIA     </td> <td>Australian Dollar</td> <td>AUD          </td> <td>6.13                         </td> <td>5.58             </td> <td>0.1      </td> <td>0.17                  </td> <td>1.03117                </td> <td>1.03142                         </td>
</tr>
<tr>
<td>AUSTRIA       </td> <td>Euro             </td> <td>EUR          </td> <td>3.32                         </td> <td>4.89             </td> <td>0.2      </td> <td>-0.52                 </td> <td>0.903896               </td> <td>0.903882                        </td>
</tr>
<tr>
<td>AZERBAIJAN    </td> <td>Azerbaijan Manat </td> <td>AZN          </td> <td>5.8                          </td> <td>4.79             </td> <td>0.18     </td> <td>-0.62                 </td> <td>0.885714               </td> <td>0.885397                        </td>
</tr>
<tr>
<td>BAHAMAS       </td> <td>Bahamian Dollar  </td> <td>BSD          </td> <td>3.75                         </td> <td>5.27             </td> <td>0.12     </td> <td>-0.14                 </td> <td>0.974026               </td> <td>0.974122                        </td>
</tr>
<tr>
<td>BAHRAIN       </td> <td>Bahraini Dinar   </td> <td>BHD          </td> <td>1.59                         </td> <td>5.95             </td> <td>0.1      </td> <td>0.54                  </td> <td>1.1013                 </td> <td>1.09982                         </td>
</tr>
<tr>
<td>BELGIUM       </td> <td>Euro             </td> <td>EUR          </td> <td>3.35                         </td> <td>4.94             </td> <td>0.21     </td> <td>-0.47                 </td> <td>0.914286               </td> <td>0.913124                        </td>
</tr>
<tr>
<td>BOLIVIA       </td> <td>Boliviano        </td> <td>BOB          </td> <td>22.08                        </td> <td>4.48             </td> <td>0.13     </td> <td>-0.93                 </td> <td>0.828571               </td> <td>0.828096                        </td>
</tr>
<tr>
<td>BRAZIL        </td> <td>Brazilian Real   </td> <td>BRL          </td> <td>11.89                        </td> <td>2.75             </td> <td>0.22     </td> <td>-2.66                 </td> <td>0.509091               </td> <td>0.508318                        </td>
</tr>
<tr>
<td>BULGARIA      </td> <td>Bulgarian Lev    </td> <td>BGN          </td> <td>4.98                         </td> <td>3.78             </td> <td>0.2      </td> <td>-1.63                 </td> <td>0.698701               </td> <td>0.698706                        </td>
</tr>
<tr>
<td>CAMBODIA      </td> <td>Riel             </td> <td>KHR          </td> <td>13083.8                      </td> <td>4.56             </td> <td>0.1      </td> <td>-0.85                 </td> <td>0.844156               </td> <td>0.842884                        </td>
</tr>
<tr>
<td>CANADA        </td> <td>Canadian Dollar  </td> <td>CAD          </td> <td>5.41                         </td> <td>5.41             </td> <td>0.109981 </td> <td>0                     </td> <td>1                      </td> <td>1                               </td>
</tr>
<tr>
<td>CHILE         </td> <td>Chilean Peso     </td> <td>CLP          </td> <td>4841.76                      </td> <td>6.95             </td> <td>0.19     </td> <td>1.54                  </td> <td>1.28571                </td> <td>1.28466                         </td>
</tr>
<tr>
<td>CHINA         </td> <td>Yuan Renminbi    </td> <td>CNY          </td> <td>30.72                        </td> <td>5.94             </td> <td>0.13     </td> <td>0.53                  </td> <td>1.0987                 </td> <td>1.09797                         </td>
</tr>
<tr>
<td>COLOMBIA      </td> <td>Colombian Peso   </td> <td>COP          </td> <td>11140.9                      </td> <td>3.51             </td> <td>0.19     </td> <td>-1.9                  </td> <td>0.649351               </td> <td>0.648799                        </td>
</tr>
<tr>
<td>COSTA RICA    </td> <td>Costa Rican Colon</td> <td>CRC          </td> <td>2144.1                       </td> <td>5.93             </td> <td>0.13     </td> <td>0.52                  </td> <td>1.0961                 </td> <td>1.09612                         </td>
</tr>
<tr>
<td>CYPRUS        </td> <td>Euro             </td> <td>EUR          </td> <td>2.83                         </td> <td>4.17             </td> <td>0.19     </td> <td>-1.24                 </td> <td>0.771429               </td> <td>0.770795                        </td>
</tr>
<tr>
<td>CZECH REPUBLIC</td> <td>Czech Koruna     </td> <td>CZK          </td> <td>94.48                        </td> <td>5.52             </td> <td>0.21     </td> <td>0.11                  </td> <td>1.02078                </td> <td>1.02033                         </td>
</tr>
</tbody>
</table>

This table now contains all the data we need to understand PPP.

The second part of this step was to map and label all countries with their currency codes; this required us to import data on the longitude and latitude of every country. We then created an if statement function to attach a specific colour to every continent based on certain conditions. This function was crucial in our process as it helped us visually distinguish between different continents. We then joined our data of currency codes and their respective countries with the imported data to map and display this information to the user.

<div style="width:100%;"><div style="position:relative;width:100%;height:0;padding-bottom:60%;"><span style="color:#565656">Make this Notebook Trusted to load map: File -&gt; Trust Notebook</span><iframe allowfullscreen="" mozallowfullscreen="" srcdoc='&lt;!DOCTYPE html&gt;
&lt;html&gt;
&lt;head&gt;
    
    &lt;meta http-equiv="content-type" content="text/html; charset=UTF-8" /&gt;
    
        &lt;script&gt;
            L_NO_TOUCH = false;
            L_DISABLE_3D = false;
        &lt;/script&gt;
    
    &lt;style&gt;html, body {width: 100%;height: 100%;margin: 0;padding: 0;}&lt;/style&gt;
    &lt;style&gt;#map {position:absolute;top:0;bottom:0;right:0;left:0;}&lt;/style&gt;
    &lt;script src="https://cdn.jsdelivr.net/npm/leaflet@1.9.3/dist/leaflet.js"&gt;&lt;/script&gt;
    &lt;script src="https://code.jquery.com/jquery-3.7.1.min.js"&gt;&lt;/script&gt;
    &lt;script src="https://cdn.jsdelivr.net/npm/bootstrap@5.2.2/dist/js/bootstrap.bundle.min.js"&gt;&lt;/script&gt;
    &lt;script src="https://cdnjs.cloudflare.com/ajax/libs/Leaflet.awesome-markers/2.0.2/leaflet.awesome-markers.js"&gt;&lt;/script&gt;
    &lt;link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/leaflet@1.9.3/dist/leaflet.css"/&gt;
    &lt;link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/bootstrap@5.2.2/dist/css/bootstrap.min.css"/&gt;
    &lt;link rel="stylesheet" href="https://netdna.bootstrapcdn.com/bootstrap/3.0.0/css/bootstrap-glyphicons.css"/&gt;
    &lt;link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/@fortawesome/fontawesome-free@6.2.0/css/all.min.css"/&gt;
    &lt;link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/Leaflet.awesome-markers/2.0.2/leaflet.awesome-markers.css"/&gt;
    &lt;link rel="stylesheet" href="https://cdn.jsdelivr.net/gh/python-visualization/folium/folium/templates/leaflet.awesome.rotate.min.css"/&gt;
    
            &lt;meta name="viewport" content="width=device-width,
                initial-scale=1.0, maximum-scale=1.0, user-scalable=no" /&gt;
            &lt;style&gt;
                #map_d00338a2ea93316dce07ba1c46eede42 {
                    position: relative;
                    width: 960.0px;
                    height: 500.0px;
                    left: 0.0%;
                    top: 0.0%;
                }
                .leaflet-container { font-size: 1rem; }
            &lt;/style&gt;
        
&lt;/head&gt;
&lt;body&gt;
    
    
            &lt;div class="folium-map" id="map_d00338a2ea93316dce07ba1c46eede42" &gt;&lt;/div&gt;
        
&lt;/body&gt;
&lt;script&gt;
    
    
            var map_d00338a2ea93316dce07ba1c46eede42 = L.map(
                "map_d00338a2ea93316dce07ba1c46eede42",
                {
                    center: [7.783333330000001, 32.525],
                    crs: L.CRS.EPSG3857,
                    zoom: 1,
                    zoomControl: true,
                    preferCanvas: false,
                    clusteredMarker: false,
                    includeColorScaleOutliers: true,
                    radiusInMeters: false,
                }
            );

            

        
    
            var tile_layer_4cb4afff0889649c7e5fd6f21d0ee033 = L.tileLayer(
                "https://tile.openstreetmap.org/{z}/{x}/{y}.png",
                {"attribution": "\u0026copy; \u003ca href=\"https://www.openstreetmap.org/copyright\"\u003eOpenStreetMap\u003c/a\u003e contributors", "detectRetina": false, "maxNativeZoom": 19, "maxZoom": 17, "minZoom": -1, "noWrap": false, "opacity": 1, "subdomains": "abc", "tms": false}
            );
        
    
            tile_layer_4cb4afff0889649c7e5fd6f21d0ee033.addTo(map_d00338a2ea93316dce07ba1c46eede42);
        
    
            var marker_b76d47c0b9156ad87611cb38731e2695 = L.marker(
                [42.5, 1.516667],
                {}
            ).addTo(map_d00338a2ea93316dce07ba1c46eede42);
        
    
            var icon_4d74180b40783993bc454f018f85617e = L.AwesomeMarkers.icon(
                {"extraClasses": "fa-rotate-0", "icon": "sign-blank", "iconColor": "white", "markerColor": "red", "prefix": "glyphicon"}
            );
            marker_b76d47c0b9156ad87611cb38731e2695.setIcon(icon_4d74180b40783993bc454f018f85617e);
        
    
        var popup_5c3018d0a028424a4340218d556614d5 = L.popup({"maxWidth": "100%"});

        
            
                var html_631a81afc11ae3c748eeb1bed305c104 = $(`&lt;div id="html_631a81afc11ae3c748eeb1bed305c104" style="width: 100.0%; height: 100.0%;"&gt;EUR&lt;/div&gt;`)[0];
                popup_5c3018d0a028424a4340218d556614d5.setContent(html_631a81afc11ae3c748eeb1bed305c104);
            
        

        marker_b76d47c0b9156ad87611cb38731e2695.bindPopup(popup_5c3018d0a028424a4340218d556614d5)
        ;

        
    
    
            var marker_b1b1aa49d2355d659eec81015807ac70 = L.marker(
                [-34.58333333, -58.666667],
                {}
            ).addTo(map_d00338a2ea93316dce07ba1c46eede42);
        
    
            var icon_8fa2ee240f70dfe6f40edacd0d8bb737 = L.AwesomeMarkers.icon(
                {"extraClasses": "fa-rotate-0", "icon": "sign-blank", "iconColor": "white", "markerColor": "orange", "prefix": "glyphicon"}
            );
            marker_b1b1aa49d2355d659eec81015807ac70.setIcon(icon_8fa2ee240f70dfe6f40edacd0d8bb737);
        
    
        var popup_4ad58fcd70ab0827d7a01ed8bd294136 = L.popup({"maxWidth": "100%"});

        
            
                var html_2b83eb13c233fd52309077e912783bc5 = $(`&lt;div id="html_2b83eb13c233fd52309077e912783bc5" style="width: 100.0%; height: 100.0%;"&gt;ARS&lt;/div&gt;`)[0];
                popup_4ad58fcd70ab0827d7a01ed8bd294136.setContent(html_2b83eb13c233fd52309077e912783bc5);
            
        

        marker_b1b1aa49d2355d659eec81015807ac70.bindPopup(popup_4ad58fcd70ab0827d7a01ed8bd294136)
        ;

        
    
    
            var marker_45c853ec6c2551228390da42ef620e84 = L.marker(
                [-35.26666667, 149.133333],
                {}
            ).addTo(map_d00338a2ea93316dce07ba1c46eede42);
        
    
            var icon_01e64a5f21cea99266968f85234bb7dc = L.AwesomeMarkers.icon(
                {"extraClasses": "fa-rotate-0", "icon": "sign-blank", "iconColor": "white", "markerColor": "black", "prefix": "glyphicon"}
            );
            marker_45c853ec6c2551228390da42ef620e84.setIcon(icon_01e64a5f21cea99266968f85234bb7dc);
        
    
        var popup_95a6c92c6a4d19a2b378bb581fa371b8 = L.popup({"maxWidth": "100%"});

        
            
                var html_504daded354ece1cc9883a19c6ef19f6 = $(`&lt;div id="html_504daded354ece1cc9883a19c6ef19f6" style="width: 100.0%; height: 100.0%;"&gt;AUD&lt;/div&gt;`)[0];
                popup_95a6c92c6a4d19a2b378bb581fa371b8.setContent(html_504daded354ece1cc9883a19c6ef19f6);
            
        

        marker_45c853ec6c2551228390da42ef620e84.bindPopup(popup_95a6c92c6a4d19a2b378bb581fa371b8)
        ;

        
    
    
            var marker_eb66e284025c12da013763624eb6059c = L.marker(
                [48.2, 16.366667],
                {}
            ).addTo(map_d00338a2ea93316dce07ba1c46eede42);
        
    
            var icon_4b29e77684cf4a51a163687c5d1dbe44 = L.AwesomeMarkers.icon(
                {"extraClasses": "fa-rotate-0", "icon": "sign-blank", "iconColor": "white", "markerColor": "red", "prefix": "glyphicon"}
            );
            marker_eb66e284025c12da013763624eb6059c.setIcon(icon_4b29e77684cf4a51a163687c5d1dbe44);
        
    
        var popup_d8fc01d8b5f728c7619cad5d6d40d58b = L.popup({"maxWidth": "100%"});

        
            
                var html_8fdc232116d9f284170096f7ca1909ba = $(`&lt;div id="html_8fdc232116d9f284170096f7ca1909ba" style="width: 100.0%; height: 100.0%;"&gt;EUR&lt;/div&gt;`)[0];
                popup_d8fc01d8b5f728c7619cad5d6d40d58b.setContent(html_8fdc232116d9f284170096f7ca1909ba);
            
        

        marker_eb66e284025c12da013763624eb6059c.bindPopup(popup_d8fc01d8b5f728c7619cad5d6d40d58b)
        ;

        
    
    
            var marker_2fd1358543055d63403f03ec4d676620 = L.marker(
                [40.38333333, 49.866667],
                {}
            ).addTo(map_d00338a2ea93316dce07ba1c46eede42);
        
    
            var icon_91d6e3c2beaf501f11247de4bd854ae0 = L.AwesomeMarkers.icon(
                {"extraClasses": "fa-rotate-0", "icon": "sign-blank", "iconColor": "white", "markerColor": "red", "prefix": "glyphicon"}
            );
            marker_2fd1358543055d63403f03ec4d676620.setIcon(icon_91d6e3c2beaf501f11247de4bd854ae0);
        
    
        var popup_c627c4015465ba72d9b94749acc46c13 = L.popup({"maxWidth": "100%"});

        
            
                var html_f9dc68ba06a83908c552ee0ae9f1791f = $(`&lt;div id="html_f9dc68ba06a83908c552ee0ae9f1791f" style="width: 100.0%; height: 100.0%;"&gt;AZN&lt;/div&gt;`)[0];
                popup_c627c4015465ba72d9b94749acc46c13.setContent(html_f9dc68ba06a83908c552ee0ae9f1791f);
            
        

        marker_2fd1358543055d63403f03ec4d676620.bindPopup(popup_c627c4015465ba72d9b94749acc46c13)
        ;

        
    
    
            var marker_b6099ad28af0282fbc0b647f794859d1 = L.marker(
                [25.08333333, -77.35],
                {}
            ).addTo(map_d00338a2ea93316dce07ba1c46eede42);
        
    
            var icon_d1732cc468bbe6da53737c1501d7d5c6 = L.AwesomeMarkers.icon(
                {"extraClasses": "fa-rotate-0", "icon": "sign-blank", "iconColor": "white", "markerColor": "grey", "prefix": "glyphicon"}
            );
            marker_b6099ad28af0282fbc0b647f794859d1.setIcon(icon_d1732cc468bbe6da53737c1501d7d5c6);
        
    
        var popup_36b8057d2cec301aa39c1babadf529b5 = L.popup({"maxWidth": "100%"});

        
            
                var html_4b7fe2d359a330d06bee6a11d216c343 = $(`&lt;div id="html_4b7fe2d359a330d06bee6a11d216c343" style="width: 100.0%; height: 100.0%;"&gt;BSD&lt;/div&gt;`)[0];
                popup_36b8057d2cec301aa39c1babadf529b5.setContent(html_4b7fe2d359a330d06bee6a11d216c343);
            
        

        marker_b6099ad28af0282fbc0b647f794859d1.bindPopup(popup_36b8057d2cec301aa39c1babadf529b5)
        ;

        
    
    
            var marker_7f96fe5e27d07f438b4dc56cd5b3384b = L.marker(
                [26.23333333, 50.566667],
                {}
            ).addTo(map_d00338a2ea93316dce07ba1c46eede42);
        
    
            var icon_e3d97936dac46b0a9c5762504d02e85c = L.AwesomeMarkers.icon(
                {"extraClasses": "fa-rotate-0", "icon": "sign-blank", "iconColor": "white", "markerColor": "green", "prefix": "glyphicon"}
            );
            marker_7f96fe5e27d07f438b4dc56cd5b3384b.setIcon(icon_e3d97936dac46b0a9c5762504d02e85c);
        
    
        var popup_1895748596a49c3dae6c0050a56564b8 = L.popup({"maxWidth": "100%"});

        
            
                var html_f3962de05e2821439eefea5b7df1cfb3 = $(`&lt;div id="html_f3962de05e2821439eefea5b7df1cfb3" style="width: 100.0%; height: 100.0%;"&gt;BHD&lt;/div&gt;`)[0];
                popup_1895748596a49c3dae6c0050a56564b8.setContent(html_f3962de05e2821439eefea5b7df1cfb3);
            
        

        marker_7f96fe5e27d07f438b4dc56cd5b3384b.bindPopup(popup_1895748596a49c3dae6c0050a56564b8)
        ;

        
    
    
            var marker_fa9affef6bf9305ea2b3acc7e695c96f = L.marker(
                [50.83333333, 4.333333],
                {}
            ).addTo(map_d00338a2ea93316dce07ba1c46eede42);
        
    
            var icon_52409bfff00c9e1593588bdc4e94c15f = L.AwesomeMarkers.icon(
                {"extraClasses": "fa-rotate-0", "icon": "sign-blank", "iconColor": "white", "markerColor": "red", "prefix": "glyphicon"}
            );
            marker_fa9affef6bf9305ea2b3acc7e695c96f.setIcon(icon_52409bfff00c9e1593588bdc4e94c15f);
        
    
        var popup_cd5c4e0178c64a381a68b87558d37f96 = L.popup({"maxWidth": "100%"});

        
            
                var html_9e3e6505edf399cca90faa74935dee25 = $(`&lt;div id="html_9e3e6505edf399cca90faa74935dee25" style="width: 100.0%; height: 100.0%;"&gt;EUR&lt;/div&gt;`)[0];
                popup_cd5c4e0178c64a381a68b87558d37f96.setContent(html_9e3e6505edf399cca90faa74935dee25);
            
        

        marker_fa9affef6bf9305ea2b3acc7e695c96f.bindPopup(popup_cd5c4e0178c64a381a68b87558d37f96)
        ;

        
    
    
            var marker_eec6ee0741132ab7fd1ed331f3ecb3c9 = L.marker(
                [-16.5, -68.15],
                {}
            ).addTo(map_d00338a2ea93316dce07ba1c46eede42);
        
    
            var icon_1f4c8bcf0e26fe8caafd0626bc424e8c = L.AwesomeMarkers.icon(
                {"extraClasses": "fa-rotate-0", "icon": "sign-blank", "iconColor": "white", "markerColor": "orange", "prefix": "glyphicon"}
            );
            marker_eec6ee0741132ab7fd1ed331f3ecb3c9.setIcon(icon_1f4c8bcf0e26fe8caafd0626bc424e8c);
        
    
        var popup_86891d1de09959dcbac0cb9aa48f3272 = L.popup({"maxWidth": "100%"});

        
            
                var html_8bf49f49810e5b57b87a85bc7712dbf2 = $(`&lt;div id="html_8bf49f49810e5b57b87a85bc7712dbf2" style="width: 100.0%; height: 100.0%;"&gt;BOB&lt;/div&gt;`)[0];
                popup_86891d1de09959dcbac0cb9aa48f3272.setContent(html_8bf49f49810e5b57b87a85bc7712dbf2);
            
        

        marker_eec6ee0741132ab7fd1ed331f3ecb3c9.bindPopup(popup_86891d1de09959dcbac0cb9aa48f3272)
        ;

        
    
    
            var marker_971f3bb36a87748af07b50b8226f0e93 = L.marker(
                [-15.78333333, -47.916667],
                {}
            ).addTo(map_d00338a2ea93316dce07ba1c46eede42);
        
    
            var icon_00fe82647d7ae11cdc3354afdc31eb5d = L.AwesomeMarkers.icon(
                {"extraClasses": "fa-rotate-0", "icon": "sign-blank", "iconColor": "white", "markerColor": "orange", "prefix": "glyphicon"}
            );
            marker_971f3bb36a87748af07b50b8226f0e93.setIcon(icon_00fe82647d7ae11cdc3354afdc31eb5d);
        
    
        var popup_01360af8a874d3f4e17c720fd4fd3e8a = L.popup({"maxWidth": "100%"});

        
            
                var html_e2c5fa73e43206b717676f344710396b = $(`&lt;div id="html_e2c5fa73e43206b717676f344710396b" style="width: 100.0%; height: 100.0%;"&gt;BRL&lt;/div&gt;`)[0];
                popup_01360af8a874d3f4e17c720fd4fd3e8a.setContent(html_e2c5fa73e43206b717676f344710396b);
            
        

        marker_971f3bb36a87748af07b50b8226f0e93.bindPopup(popup_01360af8a874d3f4e17c720fd4fd3e8a)
        ;

        
    
    
            var marker_9d530fc0de458f9de808c25afb4952e3 = L.marker(
                [42.68333333, 23.316667],
                {}
            ).addTo(map_d00338a2ea93316dce07ba1c46eede42);
        
    
            var icon_bb84aafd34007c7ba82b44e7d77a9d54 = L.AwesomeMarkers.icon(
                {"extraClasses": "fa-rotate-0", "icon": "sign-blank", "iconColor": "white", "markerColor": "red", "prefix": "glyphicon"}
            );
            marker_9d530fc0de458f9de808c25afb4952e3.setIcon(icon_bb84aafd34007c7ba82b44e7d77a9d54);
        
    
        var popup_08c1b4fed8848b8859848feb5e0a9b4a = L.popup({"maxWidth": "100%"});

        
            
                var html_a9c0743d1c2ed1739c9e8f0d1e577f96 = $(`&lt;div id="html_a9c0743d1c2ed1739c9e8f0d1e577f96" style="width: 100.0%; height: 100.0%;"&gt;BGN&lt;/div&gt;`)[0];
                popup_08c1b4fed8848b8859848feb5e0a9b4a.setContent(html_a9c0743d1c2ed1739c9e8f0d1e577f96);
            
        

        marker_9d530fc0de458f9de808c25afb4952e3.bindPopup(popup_08c1b4fed8848b8859848feb5e0a9b4a)
        ;

        
    
    
            var marker_c0f9ea6499c58d8706b09285ad84ca08 = L.marker(
                [11.55, 104.916667],
                {}
            ).addTo(map_d00338a2ea93316dce07ba1c46eede42);
        
    
            var icon_b36d25c4b614bd305eb3906364421eae = L.AwesomeMarkers.icon(
                {"extraClasses": "fa-rotate-0", "icon": "sign-blank", "iconColor": "white", "markerColor": "green", "prefix": "glyphicon"}
            );
            marker_c0f9ea6499c58d8706b09285ad84ca08.setIcon(icon_b36d25c4b614bd305eb3906364421eae);
        
    
        var popup_9bbfef5030aa46fe986029b805ebbc88 = L.popup({"maxWidth": "100%"});

        
            
                var html_81a6dbd16e63dbe517a4d0960c930f0c = $(`&lt;div id="html_81a6dbd16e63dbe517a4d0960c930f0c" style="width: 100.0%; height: 100.0%;"&gt;KHR&lt;/div&gt;`)[0];
                popup_9bbfef5030aa46fe986029b805ebbc88.setContent(html_81a6dbd16e63dbe517a4d0960c930f0c);
            
        

        marker_c0f9ea6499c58d8706b09285ad84ca08.bindPopup(popup_9bbfef5030aa46fe986029b805ebbc88)
        ;

        
    
    
            var marker_bcfde36ba6d526d2f6de1c658c5a02fd = L.marker(
                [45.41666667, -75.7],
                {}
            ).addTo(map_d00338a2ea93316dce07ba1c46eede42);
        
    
            var icon_816e6b150d35638587817b382946e294 = L.AwesomeMarkers.icon(
                {"extraClasses": "fa-rotate-0", "icon": "sign-blank", "iconColor": "white", "markerColor": "grey", "prefix": "glyphicon"}
            );
            marker_bcfde36ba6d526d2f6de1c658c5a02fd.setIcon(icon_816e6b150d35638587817b382946e294);
        
    
        var popup_b2c552c6735993bd41ed6740d0565b74 = L.popup({"maxWidth": "100%"});

        
            
                var html_1372b81c1d4bccbb278bad613a27e900 = $(`&lt;div id="html_1372b81c1d4bccbb278bad613a27e900" style="width: 100.0%; height: 100.0%;"&gt;CAD&lt;/div&gt;`)[0];
                popup_b2c552c6735993bd41ed6740d0565b74.setContent(html_1372b81c1d4bccbb278bad613a27e900);
            
        

        marker_bcfde36ba6d526d2f6de1c658c5a02fd.bindPopup(popup_b2c552c6735993bd41ed6740d0565b74)
        ;

        
    
    
            var marker_96c0e10d9cc6bd49f6b5fab5eb0ec066 = L.marker(
                [-33.45, -70.666667],
                {}
            ).addTo(map_d00338a2ea93316dce07ba1c46eede42);
        
    
            var icon_a866cafe2aa8db20c7111d7786bfd157 = L.AwesomeMarkers.icon(
                {"extraClasses": "fa-rotate-0", "icon": "sign-blank", "iconColor": "white", "markerColor": "orange", "prefix": "glyphicon"}
            );
            marker_96c0e10d9cc6bd49f6b5fab5eb0ec066.setIcon(icon_a866cafe2aa8db20c7111d7786bfd157);
        
    
        var popup_722b7e832462e5be8296047f975cc449 = L.popup({"maxWidth": "100%"});

        
            
                var html_c9107b364da0a460026bbc1f066a9aba = $(`&lt;div id="html_c9107b364da0a460026bbc1f066a9aba" style="width: 100.0%; height: 100.0%;"&gt;CLP&lt;/div&gt;`)[0];
                popup_722b7e832462e5be8296047f975cc449.setContent(html_c9107b364da0a460026bbc1f066a9aba);
            
        

        marker_96c0e10d9cc6bd49f6b5fab5eb0ec066.bindPopup(popup_722b7e832462e5be8296047f975cc449)
        ;

        
    
    
            var marker_8862aecc178bc515bc9a50e31a1857b9 = L.marker(
                [39.91666667, 116.383333],
                {}
            ).addTo(map_d00338a2ea93316dce07ba1c46eede42);
        
    
            var icon_b5711c6a612e579d3c0b0a6bd9165175 = L.AwesomeMarkers.icon(
                {"extraClasses": "fa-rotate-0", "icon": "sign-blank", "iconColor": "white", "markerColor": "green", "prefix": "glyphicon"}
            );
            marker_8862aecc178bc515bc9a50e31a1857b9.setIcon(icon_b5711c6a612e579d3c0b0a6bd9165175);
        
    
        var popup_d62a6ab76ec16e8b528920fe14725904 = L.popup({"maxWidth": "100%"});

        
            
                var html_15957001aa3f10e9b0f01bbd3bf4ce64 = $(`&lt;div id="html_15957001aa3f10e9b0f01bbd3bf4ce64" style="width: 100.0%; height: 100.0%;"&gt;CNY&lt;/div&gt;`)[0];
                popup_d62a6ab76ec16e8b528920fe14725904.setContent(html_15957001aa3f10e9b0f01bbd3bf4ce64);
            
        

        marker_8862aecc178bc515bc9a50e31a1857b9.bindPopup(popup_d62a6ab76ec16e8b528920fe14725904)
        ;

        
    
    
            var marker_5ae362211eedef740f1c343fc35d1a3f = L.marker(
                [4.6, -74.083333],
                {}
            ).addTo(map_d00338a2ea93316dce07ba1c46eede42);
        
    
            var icon_8994bfa9ee686956a0ab2088a391e557 = L.AwesomeMarkers.icon(
                {"extraClasses": "fa-rotate-0", "icon": "sign-blank", "iconColor": "white", "markerColor": "orange", "prefix": "glyphicon"}
            );
            marker_5ae362211eedef740f1c343fc35d1a3f.setIcon(icon_8994bfa9ee686956a0ab2088a391e557);
        
    
        var popup_6980bd33d159e0fa251ffbf6c8b05a6d = L.popup({"maxWidth": "100%"});

        
            
                var html_5052fcd2e652e32800cd46bf1cd077cd = $(`&lt;div id="html_5052fcd2e652e32800cd46bf1cd077cd" style="width: 100.0%; height: 100.0%;"&gt;COP&lt;/div&gt;`)[0];
                popup_6980bd33d159e0fa251ffbf6c8b05a6d.setContent(html_5052fcd2e652e32800cd46bf1cd077cd);
            
        

        marker_5ae362211eedef740f1c343fc35d1a3f.bindPopup(popup_6980bd33d159e0fa251ffbf6c8b05a6d)
        ;

        
    
    
            var marker_bf5a4f7ca611613ab7bb8886469f1b50 = L.marker(
                [9.933333333, -84.083333],
                {}
            ).addTo(map_d00338a2ea93316dce07ba1c46eede42);
        
    
            var icon_86e50939db668c6c6b69ef6ae84f8dc0 = L.AwesomeMarkers.icon(
                {"extraClasses": "fa-rotate-0", "icon": "sign-blank", "iconColor": "white", "markerColor": "black", "prefix": "glyphicon"}
            );
            marker_bf5a4f7ca611613ab7bb8886469f1b50.setIcon(icon_86e50939db668c6c6b69ef6ae84f8dc0);
        
    
        var popup_89d5de6e2e099d2757bad4c9cea196cc = L.popup({"maxWidth": "100%"});

        
            
                var html_cb419e789774a8a9fe609ac498f88eea = $(`&lt;div id="html_cb419e789774a8a9fe609ac498f88eea" style="width: 100.0%; height: 100.0%;"&gt;CRC&lt;/div&gt;`)[0];
                popup_89d5de6e2e099d2757bad4c9cea196cc.setContent(html_cb419e789774a8a9fe609ac498f88eea);
            
        

        marker_bf5a4f7ca611613ab7bb8886469f1b50.bindPopup(popup_89d5de6e2e099d2757bad4c9cea196cc)
        ;

        
    
    
            var marker_4e0506b62fde1419436e03d3d9eac421 = L.marker(
                [35.16666667, 33.366667],
                {}
            ).addTo(map_d00338a2ea93316dce07ba1c46eede42);
        
    
            var icon_7db85549d3cb0ea32e6f28dae6c959d7 = L.AwesomeMarkers.icon(
                {"extraClasses": "fa-rotate-0", "icon": "sign-blank", "iconColor": "white", "markerColor": "red", "prefix": "glyphicon"}
            );
            marker_4e0506b62fde1419436e03d3d9eac421.setIcon(icon_7db85549d3cb0ea32e6f28dae6c959d7);
        
    
        var popup_edbae31975131cf15d29f4a0a3834a75 = L.popup({"maxWidth": "100%"});

        
            
                var html_1b6113d516350436594e6c2dbfcc29b3 = $(`&lt;div id="html_1b6113d516350436594e6c2dbfcc29b3" style="width: 100.0%; height: 100.0%;"&gt;EUR&lt;/div&gt;`)[0];
                popup_edbae31975131cf15d29f4a0a3834a75.setContent(html_1b6113d516350436594e6c2dbfcc29b3);
            
        

        marker_4e0506b62fde1419436e03d3d9eac421.bindPopup(popup_edbae31975131cf15d29f4a0a3834a75)
        ;

        
    
    
            var marker_0f724597aa76641bf23ca5f8f56d1fba = L.marker(
                [50.08333333, 14.466667],
                {}
            ).addTo(map_d00338a2ea93316dce07ba1c46eede42);
        
    
            var icon_11c1c80b538b41dcba6c6a8ac3c21fd2 = L.AwesomeMarkers.icon(
                {"extraClasses": "fa-rotate-0", "icon": "sign-blank", "iconColor": "white", "markerColor": "red", "prefix": "glyphicon"}
            );
            marker_0f724597aa76641bf23ca5f8f56d1fba.setIcon(icon_11c1c80b538b41dcba6c6a8ac3c21fd2);
        
    
        var popup_6aedd5f8db40a1409e0748c613ff24eb = L.popup({"maxWidth": "100%"});

        
            
                var html_fef9e121aa14e9a12ad59b1e742eab01 = $(`&lt;div id="html_fef9e121aa14e9a12ad59b1e742eab01" style="width: 100.0%; height: 100.0%;"&gt;CZK&lt;/div&gt;`)[0];
                popup_6aedd5f8db40a1409e0748c613ff24eb.setContent(html_fef9e121aa14e9a12ad59b1e742eab01);
            
        

        marker_0f724597aa76641bf23ca5f8f56d1fba.bindPopup(popup_6aedd5f8db40a1409e0748c613ff24eb)
        ;

        
    
&lt;/script&gt;
&lt;/html&gt;' style="position:absolute;width:100%;height:100%;left:0;top:0;border:none !important;" webkitallowfullscreen=""></iframe></div></div>
