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
<td>Andorra       </td> <td>3.28                 </td> <td>4.73                 </td> <td>0.851948               </td>
</tr>
<tr>
<td>Argentina     </td> <td>4.67                 </td> <td>6.74                 </td> <td>1.21299                </td>
</tr>
<tr>
<td>Aruba         </td> <td>2.22                 </td> <td>3.2                  </td> <td>0.576623               </td>
</tr>
<tr>
<td>Australia     </td> <td>3.97                 </td> <td>5.73                 </td> <td>1.03117                </td>
</tr>
<tr>
<td>Austria       </td> <td>3.48                 </td> <td>5.02                 </td> <td>0.903896               </td>
</tr>
<tr>
<td>Azerbaijan    </td> <td>3.41                 </td> <td>4.92                 </td> <td>0.885714               </td>
</tr>
<tr>
<td>Bahamas       </td> <td>3.75                 </td> <td>5.41                 </td> <td>0.974026               </td>
</tr>
<tr>
<td>Bahrain       </td> <td>4.24                 </td> <td>6.12                 </td> <td>1.1013                 </td>
</tr>
<tr>
<td>Belgium       </td> <td>3.52                 </td> <td>5.08                 </td> <td>0.914286               </td>
</tr>
<tr>
<td>Bolivia       </td> <td>3.19                 </td> <td>4.6                  </td> <td>0.828571               </td>
</tr>
<tr>
<td>Brazil        </td> <td>1.96                 </td> <td>2.83                 </td> <td>0.509091               </td>
</tr>
<tr>
<td>Bulgaria      </td> <td>2.69                 </td> <td>3.88                 </td> <td>0.698701               </td>
</tr>
<tr>
<td>Cambodia      </td> <td>3.25                 </td> <td>4.69                 </td> <td>0.844156               </td>
</tr>
<tr>
<td>Canada        </td> <td>3.85                 </td> <td>5.55                 </td> <td>1                      </td>
</tr>
<tr>
<td>Chile         </td> <td>4.95                 </td> <td>7.14                 </td> <td>1.28571                </td>
</tr>
<tr>
<td>China         </td> <td>4.23                 </td> <td>6.1                  </td> <td>1.0987                 </td>
</tr>
<tr>
<td>Colombia      </td> <td>2.5                  </td> <td>3.61                 </td> <td>0.649351               </td>
</tr>
<tr>
<td>Costa Rica    </td> <td>4.22                 </td> <td>6.09                 </td> <td>1.0961                 </td>
</tr>
<tr>
<td>Cyprus        </td> <td>2.97                 </td> <td>4.28                 </td> <td>0.771429               </td>
</tr>
<tr>
<td>Czech Republic</td> <td>3.93                 </td> <td>5.67                 </td> <td>1.02078                </td>
</tr>
</tbody>
</table>

# 3. Factoring local tax rates into the calculation
The prices we scraped do not include the tax each Starbucks location would charge the consumers. Therefore, we wanted to examine if sales tax will affect PPP. Consequently, we scraped the sales tax in every country from Wikipedia; since the data was split into Euro and Non-Euro tables, we combined the two tables. Then, we needed to incorporate sales tax into the calculation, which sounded to us more straightforward than it was. It was more complicated than we thought because some countries have sales tax included in their price, and some do not; some countries have provinces, states, and cities that could charge different sales taxes within the same country. To tackle the tax challenge, we took the average sales tax that a consumer will pay in a country. For example, Brazil and Canada happened to have sales taxes that vary with location; therefore, we readjusted their sales tax accordingly. Using the tax data we gathered, we calculated a new PPP that includes sales tax and saved it in a new column. 

This resulted in the following table:

<table border="0" class="dataframe">
<thead>
<tr>
<th>Country</th> <th>Latte Price (USD)</th> <th>Latte Price (CAD)</th> <th>Purchasing Power Parity</th> <th>Sales Tax</th> <th>Purchasing Power Parity With Tax</th>
</tr>
</thead>
<tbody>
<tr>
<td>ANDORRA       </td> <td>3.28             </td> <td>4.73             </td> <td>0.851948               </td> <td>0.045    </td> <td>0.852252                        </td>
</tr>
<tr>
<td>ARGENTINA     </td> <td>4.67             </td> <td>6.74             </td> <td>1.21299                </td> <td>0.21     </td> <td>1.21441                         </td>
</tr>
<tr>
<td>AUSTRALIA     </td> <td>3.97             </td> <td>5.73             </td> <td>1.03117                </td> <td>0.1      </td> <td>1.03243                         </td>
</tr>
<tr>
<td>AUSTRIA       </td> <td>3.48             </td> <td>5.02             </td> <td>0.903896               </td> <td>0.2      </td> <td>0.904505                        </td>
</tr>
<tr>
<td>AZERBAIJAN    </td> <td>3.41             </td> <td>4.92             </td> <td>0.885714               </td> <td>0.18     </td> <td>0.886486                        </td>
</tr>
<tr>
<td>BAHAMAS       </td> <td>3.75             </td> <td>5.41             </td> <td>0.974026               </td> <td>0.12     </td> <td>0.974775                        </td>
</tr>
<tr>
<td>BAHRAIN       </td> <td>4.24             </td> <td>6.12             </td> <td>1.1013                 </td> <td>0.1      </td> <td>1.1027                          </td>
</tr>
<tr>
<td>BELGIUM       </td> <td>3.52             </td> <td>5.08             </td> <td>0.914286               </td> <td>0.21     </td> <td>0.915315                        </td>
</tr>
<tr>
<td>BOLIVIA       </td> <td>3.19             </td> <td>4.6              </td> <td>0.828571               </td> <td>0.13     </td> <td>0.828829                        </td>
</tr>
<tr>
<td>BRAZIL        </td> <td>1.96             </td> <td>2.83             </td> <td>0.509091               </td> <td>0.22     </td> <td>0.50991                         </td>
</tr>
<tr>
<td>BULGARIA      </td> <td>2.69             </td> <td>3.88             </td> <td>0.698701               </td> <td>0.2      </td> <td>0.699099                        </td>
</tr>
<tr>
<td>CAMBODIA      </td> <td>3.25             </td> <td>4.69             </td> <td>0.844156               </td> <td>0.1      </td> <td>0.845045                        </td>
</tr>
<tr>
<td>CANADA        </td> <td>3.85             </td> <td>5.55             </td> <td>1                      </td> <td>0.109981 </td> <td>1                               </td>
</tr>
<tr>
<td>CHILE         </td> <td>4.95             </td> <td>7.14             </td> <td>1.28571                </td> <td>0.19     </td> <td>1.28649                         </td>
</tr>
<tr>
<td>CHINA         </td> <td>4.23             </td> <td>6.1              </td> <td>1.0987                 </td> <td>0.13     </td> <td>1.0991                          </td>
</tr>
<tr>
<td>COLOMBIA      </td> <td>2.5              </td> <td>3.61             </td> <td>0.649351               </td> <td>0.19     </td> <td>0.65045                         </td>
</tr>
<tr>
<td>COSTA RICA    </td> <td>4.22             </td> <td>6.09             </td> <td>1.0961                 </td> <td>0.13     </td> <td>1.0973                          </td>
</tr>
<tr>
<td>CYPRUS        </td> <td>2.97             </td> <td>4.28             </td> <td>0.771429               </td> <td>0.19     </td> <td>0.771171                        </td>
</tr>
<tr>
<td>CZECH REPUBLIC</td> <td>3.93             </td> <td>5.67             </td> <td>1.02078                </td> <td>0.21     </td> <td>1.02162                         </td>
</tr>
</tbody>
</table>

To validate our expectation that there will be little to no difference between the PPP without tax and the PPP with tax, we created a bar graph that displays both indexes for each country side by side.

<img alt="No description has been provided for this image" class="" src="data:image/png;base64,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5p6oIPksYGKxGFZWVpg1a5bSLGtERERE9HFhQomIiIiIiIiIiNTCotxERERERERERKQWJpSIiIiIiIiIiEgtTCgREREREREREZFamFAiIo3KysrCnTt3kJWVpelQKgy2mfrYZupjm5UO2019bDMiIqKKiQklItK4vLw8TYdQ4bDN1Mc2Ux/brHTYbupjmxEREVU8TCgREREREREREZFamFAiIiIiIiIiIiK1MKFERERERERERERqYUKJiIiIiIiIiIjUwoQSERERERERERGphQklIiIiIiIiIiJSi46mAyAiIiIiIs2QSqXIzMxEVlaWpkMhIiIN09XVRbVq1aClVbK+R0woERERERF9hKRSKZ49ewZ9fX3UqlULIpFI0yEREZGGyGQyZGVl4dmzZ6hZs2aJkkoc8kZERERE9BHKzMyEvr4+9PT0mEwiIvrIiUQi6OnpQV9fH5mZmSXahwklIiIiIqKPUFZWFnR1dTUdBhERvUd0dXVLPAyaCSUiIiIioo8UeyYREVFB6vxeYEKJiIiIiIiIiIjUwoQSERERERERERGphQklIiIiIiIiIiJSCxNKRERERERE76HIyEiIxWJ4enpqOhRYW1vD2tpa02HQe8LT0xNisRiRkZGaDoU0SEfTARARERER0fvnyX/PkZySrukwVKpVwwBmJkal3v/+/fto2bKlwrJKlSrBxMQEtra2+Oabb2BlZfW2YVI58vT0hJeXl8KyqlWron79+ujXrx+mTZuGatWqaSi6dyMyMhL9+vVTWFalShWYmZmha9eumDFjBurVq/fO4pG/roYPHw5vb+93dl7SHCaUiIiIiIhISXJKOhau8td0GCrNner6VgkluQYNGmDYsGEAgMzMTJw5cwY7d+7EgQMHsG/fPtjY2Lz1OT4U+/fv13QIKvXv3x/NmjUDACQlJeHgwYPw8vJCSEgIDh06hMqVK2s4wvLXqlUr9OrVCwCQlpaGqKgobN26Ffv370d4eDg+/fTTMj/nhAkTMHjwYNStW7fMj00VBxNKRERERET0UbK0tMScOXMUli1atAhLly7FwoULERQUpKHI3j8NGjTQdAgqffnllxg8eLDw/cKFC9GjRw9cuHABO3bsgJubmwajezdat26tcB/LZDJMmjQJgYGBWLp0abn0FqpZsyZq1qxZ5selioU1lIiIiIiIiP7fhAkTAABx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KwtJSUkICwt7x9ETERERERERvX/YQ0lD/P39IZVKYWtri4YNGyqtf/36NQICAiCRSDBp0qQij9W4cWOMGzdO6HE0Y8YMYd2IESOwY8cOrFmzBsOGDdPIp3yNGjWCu7s7Nm3ahG3btr3z89eoUQPffPMN5s+fr3K4IPC/3mI9e/ZUWW8qLS0N+/fvh0QigaOjY7nGS0RERERERPS+Y0JJA2QyGfz8/CASieDt7a00FE3u9u3biImJQVxcHFq3bl3kMb/99lts3rwZq1atwvjx42FgYAAgf/jc4MGDsWvXLowYMQJr1qyBqamp0v7p6elvfV1FmT17NgIDA/Hbb79ppJfSpEmT4OPjgzVr1kBPT09h3YsXL7B3715Uq1YNmzZtgr6+vtL+UqkU1tbWOHToEJKSklS2IREREREREdHHggklDTh+/Dju37+Pzp07F5pMAgA3NzfExMRAIpEUm1AyMTHBmDFjsGbNGqxduxazZ88W1q1evRpaWlrYsWMHWrZsCXt7ezRu3BiVK1fGf//9h3PnziE+Ph41a9ZE48aNlY59584deHp6Fnrub7/9ttieT6ampvj666+xdOnSIrcrL3p6epg9ezamTZuGjIwMhXW7d+/GixcvMHz4cJXJJADQ0tKCi4sLli1bhoCAAHzzzTfvIGoiIiIiIiKi9xNrKGmAfHiVq6trkdsNHDgQenp62LlzJ169elXscadPn46qVati7dq1SE1NFZbr6enBx8cHBw4cwJdffombN2/in3/+wZo1a3DkyBHUrVsXy5YtQ1xcHNq3b6903Lt378LLy6vQf1lZWSW67mnTpqFmzZol2rY8uLm5oUmTJkrLfX19ART/85Cvl29PRERERERE9LESpaamyjQdBNGHRu/hfIikmZoOo0KQ5knxKusV9HT1OCNSCbHN1Mc2Ux/brHTYbuorqs2yjCdAqqtca5KIiIg0j3/pEBERERERERGRWphQIiIiIiIiIiIitTChREREREREREREamFCiYiIiIiIiIiI1MKEEhERERERERERqYUJJSIiIiIiIiIiUouOpgMg+hBl1XSHCFJNh1EhSPPy8OrVS4j0qkJLW1vT4VQIbDP1sc3UxzYrHbab+opqM5m2WDNBERERUbGYUCIqBzJdS8g0HUQFkZWVhYcpCTDXN4eurq6mw6kQ2GbqY5upj21WOmw39bHNiIiIKiYOeSMiIiIiIiIiIrUwoURERERERERERGphQomIiIiIiIiIiNTChBIREREREREREamFCSUiIiIiIiIiIlILZ3kjKgfxtx4gL0+q6TAqBKk0Dy9fZuPV3YfQ0uIU2yXBNlMf20x9bLPSKU271aphADMTo3KOjIiIiKhsMaFEVA6WbdiNjBcvNR1GhSCV5uHVqyzo6enyobWE2GbqY5upj21WOqVpt7lTXZlQIiIiogqHQ96IiIiIiIiIiEgtTCgREREREREREZFamFAiIiIiIiIiIiK1MKFERERERERERERqYUKJiIiIiIiIiIjUwoQSERERERERERGphQklIiIiIiIiIiJSCxNK7zkPDw+IxWI0aNAA2dnZKrextraGWCwu8jiFbZOQkIAZM2agTZs2MDU1RZ06ddCiRQsMGzYMf/75JzIzMxX2L+m/+/fvA4DS8po1a6JRo0ZwdnbGsWPHir3+fv36QSwWw9bWttjrMzU1LfZ48pjat29f6HqZTIbWrVtDLBZj2LBhJTomERERERER0cdER9MBUOEyMjKwd+9eiEQipKSkICgoCIMGDSqz41+6dAl9+/ZFWloabGxs4ODgAH19fSQmJiI6OhphYWHo378/LC0tMXnyZKSlpSns7+/vj4SEBEyaNAmGhoYK6wp+b2RkhPHjxwMAsrOzER8fj7CwMISGhmLDhg0YMmSIyvju3buHqKgoiEQixMfH48yZM2jXrl2ZXX9hIiMjcffuXYhEIoSHh+Px48f45JNPyv28RERERERERBUFE0rvsT179iAzMxMeHh7w9vaGRCIp04TSTz/9hLS0NKxbtw4uLi5K62NiYmBkZAQA+Prrr5XWR0VFISEhAZMnT0a9evUKPU/NmjUxZ84chWW7du3C2LFjMX/+/EITSr6+vpDJZJg6dSpWrVoFiUTyThJKvr6+AIApU6Zg1apV8Pf3x4wZM8r9vEREREREREQVBYe8vcckEgl0dHQwffp02NvbIyIiAg8ePCiz48fGxsLQ0FBlMgkAOnToUOxQutIaNGgQqlWrhoSEBDx79kxpfV5eHvz9/WFkZIS5c+fC0tISu3fvFobglZfU1FTs378fn332GX788UdUr15dSGwRERERERERUT4mlN5T165dQ2xsLLp37w4TExO4uLhAKpXCz8+vzM5hZGSEzMxMPH78uMyOWRra2tpKy8LDw/Ho0SMMGjQIlStXhrOzszAEsDzt3LkTWVlZcHFxgZ6eHvr374+7d+8iKiqqXM9LREREREREVJFwyNt7SiKRAACcnZ0B5BennjlzJvz8/DBr1ixoab19LnDAgAFYs2YNevfujTFjxsDW1hZWVlaoWrXqWx+7OLt27UJmZiaaNWumshfUm9fv7OyM33//Hb6+vnBzcyu3uCQSCbS0tDB06FDhvH5+fpBIJLC3ty/xcWTSPEileeUV5gdFKpUq/E/FY5upj22mPrZZ6ZSm3aTSPGRlZZVXSO+9nJwchf8/RLq6upoOgYiIqMwxofQeys3NRWBgIAwMDODk5AQA0NfXh5OTE7Zv345jx46he/fub32euXPnIiUlBdu2bcOvv/4KIL+3kJWVFfr27Yvx48eXyZC3Z8+ewdPTE4BiUW59fX0sW7ZMafvk5GSEhISgYcOGwmxs9evXh42NDU6ePImbN2+iUaNGbx3Xmy5evIgLFy6gW7duQhFue3t71K1bFwcOHEBaWppS8fHCLJ/hAJn0dZnHSEREHx6ptgwJCQmaDkPjkpKSNB1CudDW1oalpaWmwyAiIipzTCi9h4KDg5GcnAx3d3eFT7SGDx+O7du3QyKRlElCSVdXF2vXrsVPP/2EQ4cO4ezZszh79iwuXLiACxcuYPPmzQgKCkL9+vXf6jzPnz+Hl5eXwjJ9fX3s2bNHSBgVFBAQgNzcXKF3kpyLiwtOnjwJX19fzJ8//61iUkXeK6pgTSmRSARnZ2csW7YMO3fuxNixY0t0LJPs3RBJy7fe04dCKpMiOzsbVapUgZaIo3BLgm2mPraZ+thmpVOadssyHo+qBoVPbvGhy8nJQVJSEkxNTVG5cmVNh0NEREQlJEpNTWW14ffMkCFDcPjwYQQFBaFz587CcqlUCisrKzx79gzXrl1DjRo1AAAtW7bE/fv38fz580KHwllZWeHhw4dISUkp9vx3796Fh4cHoqOj0adPHwQEBKjczsnJCSdOnMCFCxcKneVNLBajUaNGiI2NBZBf9DooKAgzZsyAoaEhjh49itq1ayvs06FDB9y8eRMXLlyAhYWFsDwtLQ1NmjSBoaEhrly5Ah2d/+VDra2t8d9//5Xo0803YwKArKwsNGnSBHl5ebhx44bCsL+bN2+iffv2aN26NY4ePVrs8QFA7+F8JpRKSJonxausV9DT1YOWNh9aS4Jtpj62mfrYZqVTmnbLMp4AqW7Dco7s/ZWVlYWEhASYm5tzaBgREVEFwr8Q3zOJiYk4cuQIgPyEjVgsFv4ZGRnh0aNHyM7ORmBgoLCPgYEBgPyeQKrIZDKkpKQI2xWnQYMGWLt2LQAgMjLybS5HiVgshpubG5YsWYKkpCTMnDlTYf3p06dx48YNyGQytGjRQuH669Wrh6ysLCQlJSEsLKxM45IPaXvx4gVq166tcF55L6q4uDhcvny5TM9LREREREREVBFxyNt7xt/fH1KpFLa2tmjYUPnTytevXyMgIAASiQSTJk0CAHz22We4dOkSYmJi4OjoqLTP5cuXkZmZiU6dOpU4Dn19/dJfRAm4u7tj48aNCA4OxunTp9GxY0cA/xt21rNnT5iZmSntl5aWhv3790Mikai81tKSn3fAgAGoXr260vpHjx4hPDwcEolEafgeERERERER0ceGCaX3iEwmg5+fH0QiEby9vQutXXT79m3ExMQgLi4OrVu3hqurKwIDA/Hbb7+hU6dOCoW0s7OzhYLbBWsDAYCXlxfc3NxQt25dpThWrFgBALCxsSm7CyxAJBJh1qxZcHV1xeLFi7F//368ePECe/fuRbVq1bBp0yaVSS2pVApra2scOnRIqLfwtu7du4fIyEhYWFhg06ZNEIlEStukpaWhadOm2L59OxYsWIAqVaq89XmJiIiIiIiIKiomlN4jx48fx/3799G5c+ciC2G7ubkhJiYGEokErVu3RteuXTFp0iSsW7cO7dq1Q58+fWBqaornz58jLCwMiYmJ6Nu3L0aMGKFwnDVr1uD3339H69at0apVK9SoUQPPnz9HZGQkbt26BSMjIyxatKjcrtfR0RGtWrXC8ePHERUVhTt37uDFixcYPnx4oT2ktLS04OLigmXLliEgIADffPONsC43NxeTJ08u9Hze3t4ql/v6+kImk2H48OEqk0kAYGhoiL59+2LHjh0ICgrCoEGDSn6hRERERERERB8YFuV+j4wbNw47d+7EmjVr4ObmVuh26enpaNKkCSpVqoTr169DT08PALB//35s2bIF58+fR1paGqpVq4bmzZvDxcUFI0aMUCrYHR0djUOHDuHEiRNISEhAcnIyqlSpgnr16qF79+7w8PBQOexMrjRFud8UEhICFxcX2NraIi8vDzExMThw4ADs7e0LPe/t27fRtm1bNGzYEGfOnAGQX5S7uCmXU1NTlWKS93h69OgR4uLiikzkHTt2DAMGDEC3bt2wZ8+eIs/Fotwlx8K/6mObqY9tpj62WemwKLf6WJSbiIioYmJCiagcMKFUcnxoVR/bTH1sM/WxzUqHCSX1MaFERERUMfEvRCIiIiIiIiIiUgsTSkREREREREREpBYmlIiIiIiIiIiISC1MKBERERERERERkVqYUCIiIiIiIiIiIrUwoURERERERERERGrR0XQARB+irJruEEGq6TAqBGleHl69egmRXlVoaWtrOpwKgW2mPraZ+thmpVOadpNpi8s3KCIiIqJywIQSUTmQ6VpCpukgKoisrCw8TEmAub45dHV1NR1OhcA2Ux/bTH1ss9JhuxEREdHHgkPeiIiIiIiIiIhILUwoERERERERERGRWphQIiIiIiIiIiIitTChREREREREREREamFCiYiIiIiIiIiI1MKEEhERERERERERqUVH0wEQfYjibz1AXp5U02FUCFJpHl6+zMaruw+hpaWt6XAqBLaZ+thm6qsobVarhgHMTIw0HQYRERHRR4cJJaJysGzDbmS8eKnpMCoEqTQPr15lQU9P971+aH2fsM3UxzZTX0Vps7lTXZlQIiIiItIADnkjIiIiIiIiIiK1MKFERERERERERERqYUKJiIiIiIiIiIjUwoQSERERERERERGphQklIiIiIiIiIiJSCxNKRERERERERESkFiaUPnIeHh4Qi8Vo0KABsrOzVW5jbW0NsVhc5HEK2yYhIQEzZsxAmzZtYGpqijp16qBFixYYNmwY/vzzT2RmZirsX9J/9+/fBwCl5TVr1kSjRo3g7OyMY8eOqYzV09MTYrEYu3btKvR6AgIChGOeO3euyGsnIiIiIiIi+tjoaDoA0pyMjAzs3bsXIpEIKSkpCAoKwqBBg8rs+JcuXULfvn2RlpYGGxsbODg4QF9fH4mJiYiOjkZYWBj69+8PS0tLTJ48GWlpaQr7+/v7IyEhAZMmTYKhoaHCuoLfGxkZYfz48QCA7OxsxMfHIywsDKGhodiwYQOGDBmiduwSiQQikQgymQy+vr5o06ZNKVqAiIiIiIiI6MPEhNJHbM+ePcjMzISHhwe8vb0hkUjKNKH0008/IS0tDevWrYOLi4vS+piYGBgZGQEAvv76a6X1UVFRSEhIwOTJ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5MgR2e32Il/h4eHq3LmzZs6cqQsXLpR4/s6dOz3nrF69usRxCQkJstvtmjdvXolj4uLiZLfblZycXOjztm3bFqotJCREkZGRuvfee0uds8ATTzwhu92uyMhI5ebmljiub9++stvtSk9P93z26/488MADxZ63d+9e2e12jRo1qsxaAAAAAACozfy8XQAurcjISA0aNEiS5Ha7lZGRoY8//lgzZ87Upk2btH79etlstiLnxcfHS5IsFoscDof69+9fLfXZbDZNmDBBkpSfn6/U1FS9//772rZtm5599ln9z//8T7HnnT9/XqtXr5bFYtGZM2e0bt26EoOhsmzevFlbt25Vt27dKnwfAAAAAADUZgRKdUxUVJQmT55c6LPc3Fz16NFDe/fu1Y4dO4oEKefOndPatWt1/fXXKzQ0VJs3b9bx48fVokWLKq/Pz8+vSH27d+9Wnz599Morr+jxxx9XcHBwkfNWrVqlixcv6oknntAbb7yh+Pj4CgVKLVu21PHjxzVt2jRt3rxZFoulwvcCAAAAAEBtxZI3KCAgQF26dJEkZWZmFjmenJys7OxsxcTEKCYmRoZhaOnSpZesvo4dO6pNmzbKycnR999/X+yY+Ph4+fn56amnnlKXLl20detWHT161PRcV199taKjo/XFF19o1apVlS0dAAAAAIBaiUAJysvL044dO2SxWNS2bdsix+Pj42Wz2TRo0CDdc889atCggRISEuR2uy95rcUtx/v3v/+tvXv36q677lJoaKgn9EpISKjQHFOmTFFAQIBmzJihn3/+ubIlAwAAAABQ67DkrY5JTU1VXFycpF/2UMrMzNSmTZt06tQpTZ8+Xa1bty40/ttvv9W+ffvUvXt3hYWFSZL69eunpKQkbdu2rcR9hrZs2SKn01nssR07dpiqeffu3Tpw4IBCQkLUpk2bIscL9neKjo6WJN1zzz2aMGGCEhISNHHiRFmt5nLTiIgIjRw5UvPnz9fbb7+tkSNHmjpfktyGS4bhMn1eXWQYRqE/UTZ6Zh49M4+eVUxN75thuEr877O35OXlFfqzNgoMDPR2CQAAVDkCpTomLS1Ns2bNKvJ5z549iw2HCsKamJgYz2eDBw9WUlKS4uPjSwyUtm7dqq1bt5quLz8/3xN4/XpTbqvVqjlz5hT5geznn3/Wu+++q4YNG6pv376SpAYNGqhv375a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v91u9zwJxubcAAAAAIC6ztQTSldeeaX27dunn376yfM0SnmcPn1aR44cUfv27U0XiIrJysqS9EtIVOC6667T119/rU8//VR9+vQpcs4333yjixcvqnPnzhWeNzY2VrNnz9bs2bP1+uuvmzq3IKjp37+/LrvssiLHT548qU2bNik+Pr7YfaN+a9iwYVq0aJE++OAD7dmzp9AStuKkpKTo0KFDioyM1B133FHsmA8//FAfffSR6f8PAAAAAABQm5gKlLp06aJ9+/Zp0aJFmjRpUrnPW7Rokdxut7p27Wq6QFRMQZjz63AoNjZW7777rl566SV17ty50N5Fubm5eu655yQV3r/IrCeffFKrV69WQkKCQkNDNXHixCKPr+fn5ys7O7vQZ4cPH9b27dvVsmVLvf3228Uuuzt79qyuueYaLVu2TNOnT1dAQECptVgsFk2cOFGxsbF68cUXtXbt2lLHFwRaBUvlijN9+nTNnTtXSUlJGjNmTKnXAwAAAACgtjIVKD388MNasGCBXn31Vd1xxx0lPsXxa9u3b9err74qPz8/PfTQQxUuFMVLTU31vN1Mks6cOaM9e/Zo//79stvtmjZtmudYt27d9Pjjj+sf//iHbrnlFvXu3VthYWHKzMzUhg0bdPz4cfXr16/EMGX16tU6cOBAscf69u2rfv36qWHDhlq5cqWGDBmiefPmacmSJbrzzjsVERGh/Px8paena+vWrTp9+rSuu+46zzJIh8Mht9utwYMHl7iHU6NGjdSvXz8tX75c69at0wMPPFBmf/r06aN27dpp27Zt2rFjR4n/zp47d05r1qxR/fr11b9//xKvFxsbq7lz5yo+Pp5ACQAAAABQZ5kKlFq1aqXHH39cCxYs0IABA/TUU0/pscce0+WXX15kbEZGhv7xj3/o73//u37++WeNGjVKrVq1qqq68V9paWmFln8FBAQoPDxcjzzyiMaOHauIiIhC42fOnKnOnTvrnXfe0QcffKCzZ8+qfv36uv766/W3v/1NQ4cOLXHD7v3792v//v3FHmvZsqX69evn+edPPvlEK1as0KpVq7Rz505lZmbKz89PYWFh6tKli+6//3717t1bNptNhmEoMTFRFotFgwcPLvV+hwwZouXLlys+Pr5cgZIkTZo0STExMXrxxRf14YcfFjtm5cqVys7O1uDBg0vdeL5169bq2LGjdu/eXa5ldAAAAAAA1EaWrKwsd9nD/j/DMPTQQw9p3bp1slgsslqtuuaaa9SqVSvVr19fFy9e1OHDh/Xvf/9bhmHI7XarT58+io+PLzGoAGqboBPPy2Jc9HYZPsFwGcpx5igoMKjGvX2rpqJn5tXknjmbjpQR2NrbZRThdDp17NgxRURE8OYtE+ibefQMAADfZOoJJemXV887HA7Nnz9f8+bN05kzZ/Ttt9/q22+/lcViKbQJdOPGjTV27Fg9+eSTVVo0AAAAAAAAvMd0oFRgzJgxeuSRR/Txxx9r165dOnnypM6fP6/LLrtM4eHh6tSpk+6++27Vr1+/KusFAAAAAACAl1U4UJKk4OBg3Xfffbrvvvuqqh4AAAAAAADUcDVrIwkAAAAAAADUeARKAAAAAAAAMIVACQAAAAAAAKZUag8lAMVzXj5MFhneLsMnGC6XcnKyZQkKltVm83Y5PoGemVeTe+a22b1dAgAAAGAagRJQDdyBUXJ7uwgf4XQ6deLMMUU0iFBgYKC3y/EJ9Mw8egYAAABULZa8AQAAAAAAwBQCJQAAAAAAAJhCoAQAAAAAAABTCJQAAAAAAABgCoESAAAAAAAATOEtb0A1+O7QUblchrfL8AmG4VJ2dq5y0k7Iaq1Zr3OvqeiZefTMvKrsWZPGDdUsNKSKKgMAAEBNQKAEVIM5b63U+QvZ3i7DJxiGSzk5TgUFBfKLfjnRM/PomXlV2bNnxsQSKAEAANQyLHkDAAAAAACAKQRKAAAAAAAAMIVACQAAAAAAAKYQKAEAAAAAAMAUAiUAAAAAAACYQqAEAAAAAAAAUwiUAAAAAAAAYAqBko/48ssvNXr0aLVv317h4eFq1qyZ2rVrp5EjR+qTTz4p9pyLFy8qIiJCdrtdEyZMKPHaR44ckd1ul91uV5s2bZSfn1/suO+//94zrm3btoWOJSQkeI4VfDVu3FgtW7ZU79695XA4Spzf5XLJ4XCof//+uuqqq9S0aVO1adNG0dHRWrNmTYnn/Xa+Zs2aqU2bNurVq5emTp2qr7/+utT7HTBgQInXLm/vAAAAAACoi/y8XQBKZxiGpk6dqoULF8rPz09du3ZV7969Va9ePR0+fFgbNmzQsmXLNGXKFP3tb38rdO6qVat0/vx5WSwWLV++XDNmzFBgYGCJc/n5+en06dPasGGD+vTpU+R4fHy8rNbSM8hu3bqpY8eOkn4Jio4fP64PPvhAo0eP1vfff68XXnih0PiffvpJsbGx2rt3r5o1a6Y+ffqoadOmOnHihDZs2KCPPvpIvXr10qJFi1S/fv0i84WEhOjRRx+VJOXn5ysjI0NfffWVFixYoAULFmjo0KGaM2eOAgICSq37t8z2DgAAAACAuoRAqYabMWOGFi5cqLZt22rJkiWKjIwsdDwnJ0dvvvmmMjMzi5zrcDjk5+enRx99VG+88Ybee+89DRw4sMS5br31Vn3zzTdyOBxFAqX8/HwtW7ZMd955p3bu3FniNe68806NGzeu0GdHjhxR586d9X//93+aMmWKgoKCJEk///yzhgwZor1792rYsGF6+eWXPcckKSsrS4899pjWr1+vJ554QosXLy4y3+WXX67JkycX+fxf//qXHnvsMTkcDuXl5en//u//Sqy5OGZ7BwAAAABAXcKStxosNTVVr732mkJCQpScnFwkTJKkoKAgPfnkk0VClYMHD2r37t3q3r27/vKXv8hisSg+Pr7U+YKCgjRgwABt2LBBP/30U6Fj69ev1+nTpzV06FDT93HllVeqdevWys3N1YULFzyfJyYm6tNPP1WnTp3097//vVCYJP2ypG3x4sWKiorS6tWrtXXr1nLPed1112nVqlVq0qSJli1bps8//7zc51akdwAAAAAA1CUESjXY0qVL5XK5NGLECIWGhpY69rdLugoCkMGDBysiIkJ33HGHtm/frsOHD5d6naFDhyo/P19JSUmFPnc4HGrcuLH69u1r+j6OHj2qQ4cOqXnz5mratKnn84SEBEnShAkTZLFYij03KChIo0ePLjS+vJo0aaIRI0ZIklauXFnu8yraOwAAAAAA6gqWvNVgu3fvliR17drV1HkFgVCjRo3Uq1cvSVJ0dLS2b98uh8OhqVOnlnjuzTffrOuuu05Lly7VmDFjJEnp6enauHGj/vSnP5W5F9GWLVvkdDol/bKH0okTJ/Thhx8qODhYCxcuLFTjvn375Ofnp9tvv73Ua3br1k2S9Omnn5Z9879xxx136JVXXtG+ffvKNb4yvfs1t+GSYbhM11sXGYZR6E+UjZ6ZR8/Mq8qeGYbL89+G2i4vL6/QnyhbXegZ+zACAGojAqUa7PTp05Kk8PBwU+cVLE97+OGHPT/A3Hffffrb3/6mxMRETZkypdTNtYcMGaKnn35an332mW655RYlJiYqPz+/XMvdtm7dWmRpmp+fn0aMGKHrrrvO81lmZqZ+/vlnhYWFlflDVvPmzSX9EmyZdcUVV3jmK4/K9q7A3PF3y20U/7Y8AKhrDJtbx44d83YZl1RF/ptV19XWntlsNkVFRXm7DAAAqhyBUi1UsGQrJibG89lll12mvn37avny5dq0aZN69OhR4vnR0dGaNm2aHA6HbrnlFiUkJOiGG27QDTfcUObczz33nGdTbsMw9OOPP2rdunWaOnWqPv74Y23dulWNGjWq5B1Wn8r2rkBo7kpZjIvVVmdtYrgN5ebmKiAgQFYLq3DLg56ZR8/Mq8qeOZs+quCGV1ZRZTVbXl6e0tPTFRYWJn9/f2+X4xPoGQAAvolAqQYLDQ3VgQMHdPLkSV199dXlOufUqVPauHGjWrVqpU6dOhU6FhMTo+XLl8vhcJQaijRp0kS9evXSypUr1b9/fx08eFAvv/yy6fqtVqvCw8P16KOPKj09XbNnz9abb76pCRMmKCQkRPXq1VNGRoacTmepTymdOHFCkhQWFma6hlOnTkn65W1w5Rlb2d4VsNqssvBLa/n8d2Wg1WKV1UbPyoWemUfPzKvCnllttjq35Mff37/O3XNl0TMAAHwLP1XXYB07dpQkbdu2rdznFGzkffjwYdnt9kJfAwYMkCR9+OGHysjIKPU6w4YN07lz5/SXv/xFgYGBGjRoUMVvRL/szSTJs5eRn5+f2rdvr/z8fO3cubPUcwuW0N16662m592xY4ckqX379mWOrareAQAAAABQ2/GEUg0WGxurefPmafHixRo1apSaNGlS4tjc3Fz5+/vL4XB4zrXZbEXGHThwQHv27FFSUpKeeOKJEq/XvXt3hYeH6+TJkxowYIDsdnul7iUrK0tS4c1dY2NjtWfPHs2dO1d33XVXsW96czqdev311yX9sreTGf/5z3+0ePFiSfIEQiVxu91V1jsAAAAAAGo7AqUaLCoqSk899ZTmzp2rBx98UIsXL1arVq0KjXE6nXrrrbeUkZGhu+66S2lpaercuXOhN6r92sGDB9WhQwc5HI5SQxGbzaaEhASdOHFCbdu2rdR9OJ1OLVq0SJIKvdEtNjZW8fHx2rlzp8aNG6eZM2cWetT97Nmzevzxx/XDDz+of//+nre9lcd3332nkSNH6qefftLgwYN10003lTp+x44dVdY7AAAAAABqOwKlGm7q1KlyOp1auHChOnTooK5du+raa69VvXr1dOTIEW3ZskWZmZmaOnWqZ0Pp0p7kufrqq3Xbbbdpz549nre4leSmm24qM4j5rS1btnheDW0Yhk6fPq2NGzd6gqlHHnnEM7ZevXpaunSpBg8erMWLF+ujjz5Sjx491LRpU508eVIfffSRMjMz1bNnT89TSr+VkZGhuLg4SZLL5VJmZqb279+vzz//XJL00EMPafbs2WXWXdW9AwAAAACgNiNQquGsVqteeuklDRw4UIsWLVJKSopSUlJkGIbCwsLUvXt3DRkyRDfddJOuueYa1a9fX/fdd1+p1xwyZIj27Nmj+Pj4Kg9Ftm7d6tnzSJLq16+vqKgojRgxQn/5y18UHBxcaHxoaKg++ugjLV26VCtWrND777+v8+fPy263q0OHDoqNjS31fjIzMzVr1ixJUkBAgBo2bKirrrpKY8aMUXR0tH7/+9+XWfPZs2f13nvveb13AAAAAAD4CktWVpbb20UAtU3QiedlMS56uwyfYLgM5ThzFBQYxNu3yomemUfPzKvKnjmbjpQR2LqKKqvZnE6njh07poiICN5YVk70DAAA38RP1QAAAAAAADCFQAkAAAAAAACmECgBAAAAAADAFAIlAAAAAAAAmEKgBAAAAAAAAFMIlAAAAAAAAGCKn7cLAGoj5+XDZJHh7TJ8guFyKScnW5agYFltNm+X4xPomXn0zLyq7JnbZq+aogAAAFBjECgB1cAdGCW3t4vwEU6nUyfOHFNEgwgFBgZ6uxyfQM/Mo2fm0TMAAACUhiVvAAAAAAAAMIVACQAAAAAAAKYQKAEAAAAAAMAUAiUAAAAAAACYQqAEAAAAAAAAUwiUAAAAAAAAYIqftwsAaqPvDh2Vy2V4uwyfYBguZWfnKifthKxWm7fL8Qn0zDx6Zh49qxjDcKmejb+vAwAAtR+BElAN5ry1UucvZHu7DJ9gGC7l5DgVFBTIL63lRM/Mo2fm0bOKMQyXxj9yv7fLAAAAqHb8FRoAAAAAAABMIVACAAAAAACAKQRKAAAAAAAAMIVACQAAAAAAAKYQKAEAAAAAAMAUAiUAAAAAAACYQqAEffnllxo9erTat2+v8PBwNWvWTO3atdPIkSP1ySefFHvOxYsXFRERIbvdrgkTJpR47SNHjshut8tut+uBBx4odszevXtlt9s1atSoEq9z9OhRhYSEyG636+9//3uJ47Zv3+6Zr+CrefPmuv766/Xggw9q3rx5OnXqVInnF9i5c6fn/NWrV5c5HgAAAACAuoRAqQ4zDENTpkzRnXfeqaSkJLVq1UojRozQ448/rnbt2mnDhg26//779fLLLxc5d9WqVTp//rwsFouWL18up9NZ5nybN2/W1q1bK1Srw+GQYRiyWCxyOBxljm/Xrp0mTpyoiRMn6pFHHtEdd9yhH374Qc8//7xuuukm/e///m+p58fHx0tSuecDAAAAAKAu8fN2AfCeGTNmaOHChWrbtq2WLFmiyMjIQsdzcnL05ptvKjMzs8i5DodDfn5+evTRR/XGG2/ovffe08CBA0ucq2XLljp+/LimTZumzZs3y2KxlLtOwzC0dOlSXX755erZs6eWLl2qPXv26LbbbivxnJtuukmTJ08u8vm6des0ZswYTZw4UcHBwRo2bFiRMefOndPatWt1/fXXKzQ0VJs3b9bx48fVokWLctcMAAAAAEBtxhNKdVRqaqpee+01hYSEKDk5uUiYJElBQUF68skniwQzBw8e1O7du9W9e3f95S9/kcVi8TzRU5Krr75a0dHR+uKLL7Rq1SpTtX7yySc6fvy4HnjgAU8AVNZ8Jenbt6/eeecdSdK0adN08eLFImOSk5OVnZ2tmJgYxcTEeAItAAAAAADwCwKlOmrp0qVyuVwaMWKEQkNDSx0bEBBQ6PuCMGfw4MGKiIjQHXfcoe3bt+vw4cOlXmfKlCkKCAjQjBkz9PPPP5e71l/P16lTJ7Vq1UqrV6/WhQsXyn2NX+vSpYs6deqkjIwMbdu2rdj5bDabBg0apHvuuUcNGjRQQkKC3G53heYDAAAAAKC2YclbHbV7925JUteuXU2dl5+fr6SkJDVq1Ei9evWSJEVHR2v79u1yOByaOnVqiedGRERo5MiRmj9/vt5++22NHDmyzPkyMzP1wQcfqE2bNmrfvr0kadCgQXr55Ze1cuVKPfTQQ6bqL3DHHXdo165d2rdvn3r37u35/Ntvv9W+ffvUvXt3hYWFSZL69eunpKQkbdu2Td26dSvX9d2GS4bhqlBtdY1hGIX+RNnomXn0zDx6VjEF/crLy/NyJb6joFe1uWeBgYHeLgEAgCpHoFRHnT59WpIUHh5u6rz169fr9OnTevjhhz0/HN13333629/+psTERE2ZMkVWa8kPvo0fP15LlizRK6+8otjYWDVo0KDU+ZKSkpSXl6fo6GjPZ4MHD9bLL78sh8NR4UDpiiuukKQi+0MVPA0VExNTaL6kpCTFx8eXO1CaO/5uuY38CtUGAPBthi1Q6enp3i7D59TWntlsNkVFRXm7DAAAqhyBEkwpLnC57LLL1LdvXy1fvlybNm1Sjx49Sjzfbrdr3LhxmjZtmubPn1/sxtm/5nA4ZLFYNGjQIM9nkZGRuu2227Rnzx59//33+t3vflfJu/pFbm6uli1bpssuu0z9+vXzfN6lSxe1aNFC77//vrKysmS328u8VmjuSlmMovszoSjDbSg3N1cBAQGyWliFWx70zDx6Zh49qxjDbSjrsmEKC7tK/v7+3i7HJ+Tl5Sk9PV1hYWH0DAAAH0KgVEeFhobqwIEDOnnypK6++upynXPq1Clt3LhRrVq1UqdOnQodi4mJ0fLly+VwOEoNlCTpscce05tvvqnXX39df/7zn0sc99lnn+lf//qXunTpooiIiCLz7dmzRw6HQy+88EK56v/tvUjS5Zdf7vls3bp1yszM1JAhQxQUFOT53Gq1auDAgZo3b56WL1+uRx99tMzrW21WWfgFrHz+uzLQarHKaqNn5ULPzKNn5tGzivlv3/z9/VnmZBI9AwDAt/ATYh3VsWNHSSp2U+qSFGzkffjwYdnt9kJfAwYMkCR9+OGHysjIKPU6QUFBmjRpki5cuKBZs2aVOK7gaajt27cXmW/cuHGSflkSZ2aD7wI7duyQJM++TL+eLyEhoch88+bNKzQGAAAAAIC6jCeU6qjY2FjNmzdPixcv1qhRo9SkSZMSx+bm5srf318Oh8Nzrs1mKzLuwIED2rNnj5KSkvTEE0+UOf/ChQv1zjvvqEOHDkWOX7x4UStXrlRwcLAnrPqtffv26dtvv9X69et1zz33lDrfr+3YsUO7du1S06ZNPZuSHz16VFu3blVoaKh69uxZ7Hnbtm3TV199pf379+vGG28s93wAAAAAANQ2BEp1VFRUlJ566inNnTtXDz74oBYvXqxWrVoVGuN0OvXWW28pIyNDd911l9LS0tS5c2ctXLiw2GsePHhQHTp0kMPhKDNQstlseuaZZxQbG6uZM2cWOb569WqdP39eMTExmj9/frHX2Lx5sx544AE5HI5yB0offvihp7Zp06YpODhY0i9PJRmGoeHDh2vKlCnFnrt48WKNHTtWDoeDQAkAAAAAUKcRKNVhU6dOldPp1MKFC9WhQwd17dpV1157rerVq6cjR45oy5YtyszM1NSpUz1LvYYMGVLi9a6++mrPZtmfffaZbrnlllLn79Onjzp16qRdu3YVOVbwNFRp8915551q3ry5Nm7cqFOnTnne3CZJX3zxheLi4iT98oTVjz/+qE8//VSpqakKCgrS7NmzPdc2DEMJCQmyWCyKjY0tcb77779fkydP1rJly/TCCy+wzwMAAAAAoM4iUKrDrFarXnrpJQ0cOFCLFi1SSkqKUlJSZBiGwsLC1L17dw0ZMkQ33XSTrrnmGtWvX1/33XdfqdccMmSI9uzZo/j4+DIDJemXp4R+u8Ts4MGD2rVrl6688krdcccdpdY/ePBgzZ49W0uXLtX48eM9x7788kt9+eWXkqTg4GA1btxY11xzjR566CHFxMSoWbNmnrFbtmzR8ePHdfvttxd5SuvXGjVqpHvuuUfLli3Te++9p4EDB5Z5fwAAAAAA1EaWrKwst7eLAGqboBPPy2Jc9HYZPsFwGcpx5igoMIg3SZUTPTOPnplHzyrGcBnKbDBE1gbX8iRrOTmdTh07dkwRERH0DAAAH8JPiAAAAAAAADCFQAkAAAAAAACmECgBAAAAAADAFAIlAAAAAAAAmEKgBAAAAAAAAFMIlAAAAAAAAGCKn7cLAGoj5+XDZJHh7TJ8guFyKScnW5agYFltNm+X4xPomXn0zDx6VjGGy6W8i1YFersQAACAakagBFQDd2CU3N4uwkc4nU6dOHNMEQ0iFBjIr2DlQc/Mo2fm0bOKcTqd+unsMUU09HYlAAAA1YslbwAAAAAAADCFQAkAAAAAAACmECgBAAAAAADAFAIlAAAAAAAAmEKgBAAAAAAAAFMIlAAAAAAAAGCKJSsri7ebA1Xsu0NH5XIZ3i7DJxiGS9nZOQoODpLVavN2OT6BnplHz8yjZxVD38yrKT1r0rihmoWGeG1+AAB8jZ+3CwBqozlvrdT5C9neLsMnGIZLOTlOBQUF8stXOdEz8+iZefSsYuibeTWlZ8+MiSVQAgDABJa8AQAAAAAAwBQCJQAAAAAAAJhCoAQAAAAAAABTCJQAAAAAAABgCoESAAAAAAAATCFQAgAAAAAAgCkESrhkvvzyS40ePVrt27dXeHi4mjVrpnbt2mnkyJH65JNPPOPi4uJkt9uVnJxc4rVGjRolu92uvXv3FvrcbrerQ4cOhT5LSEiQ3W7XvHnzyqyxYO7SvuLi4kzeOQAAAAAAtYuftwtA7WcYhqZOnaqFCxfKz89PXbt2Ve/evVWvXj0dPnxYGzZs0LJlyzRlyhT97W9/83a5kqR7771X1157bbHH7rjjjktcDQAAAAAANQuBEqrdjBkztHDhQrVt21ZLlixRZGRkoeM5OTl68803lZmZ6aUKi7rvvvs0YMAAb5cBAAAAAECNRKCEapWamqrXXntNISEhSk5OVmhoaJExQUFBevLJJ5Wbm+uFCgEAAAAAgFnsoYRqtXTpUrlcLo0YMaLYMOnXAgICLlFVAAAAAACgMnhCCdVq9+7dkqSuXbuaPnfNmjU6cOBAsce+/vrrStVVmbn/9Kc/KSwsrFrnBwAAAACgJiNQQrU6ffq0JCk8PNz0uWvXrtXatWuruqRKz923b98yAyW34ZJhuKqjtFrHMIxCf6Js9Mw8emYePasY+mZeTemZYbjkdDqr5dqBgYHVcl0AALyJQAk11qJFi0rcGHvUqFFKTEz0ytzlMXf83XIb+VVYEQAAqE6Gza1jx45V+XVtNpuioqKq/LoAAHgbgRKqVWhoqA4cOKCTJ0/q6quv9nY5l0xo7kpZjIveLsMnGG5Dubm5CggIkNXCtm7lQc/Mo2fm0bOKoW/m1ZSeOZs+quCGV3ptfgAAfA2BEqpVx44dtWPHDm3btk3dunXzdjmXjNVmlYVfJMrnvysDrRarrDZ6Vi70zDx6Zh49qxj6Zl4N6ZnVZmNpGgAAJvCTDqpVbGysbDabFi9erP/85z+ljs3Nzb1EVQEAAAAAgMogUEK1ioqK0lNPPaWMjAw9+OCDOnz4cJExTqdTCxYs0MyZMy99gQAAAAAAwDSWvKHaTZ06VU6nUwsXLlSHDh3UtWtXXXvttapXr56OHDmiLVu2KDMzU1OnTq3WOlavXq0DBw4Ue6xv377q16+f5/s1a9aUOLZNmzaV2rAbAAAAAABfR6CEame1WvXSSy9p4MCBWrRokVJSUpSSkiLDMBQWFqbu3btryJAhuvPOO6u1jv3792v//v3FHmvZsmWhQGnt2rVau3ZtsWP79OlDoAQAAAAAqNMsWVlZbm8XAdQ2QSee5y1v5WS4DOU4cxQUGMQGtuVEz8yjZ+bRs4qhb+bVlJ45m46UEdjaa/MDAOBr+EkHAAAAAAAAphAoAQAAAAAAwBQCJQAAAAAAAJhCoAQAAAAAAABTCJQAAAAAAABgCoESAAAAAAAATCFQAgAAAAAAgCl+3i4AqI2clw+TRYa3y/AJhsulnJxsWYKCZbXZvF2OT6Bn5tEz8+hZxdA382pKz9w2u9fmBgDAFxEoAdXAHRglt7eL8BFOp1MnzhxTRIMIBQYGerscn0DPzKNn5tGziqFv5tEzAAB8E0veAAAAAAAAYAqBEgAAAAAAAEwhUAIAAAAAAIApBEoAAAAAAAAwhUAJAAAAAAAApvCWN6AafHfoqFwuw9tl+ATDcCk7O1c5aSdktfKK7fKgZ+bRM/PoWcXU5L41adxQzUJDvF0GAACoJQiUgGow562VOn8h29tl+ATDcCknx6mgoMAa98tXTUXPzKNn5tGziqnJfXtmTCyBEgAAqDIseQMAAAAAAIApBEoAAAAAAAAwhUAJAAAAAAAAphAoAQAAAAAAwBQCJQAAAAAAAJhCoAQAAAAAAABTCJQAAAAAAABgCoESqsWXX36p0aNHq3379goPD1ezZs3Url07jRw5Up988olnXFxcnOx2u5KTk0u81qhRo2S327V3795Cn9vtdnXo0KHQZwkJCbLb7bLb7Zo7d26x15s3b57sdrsSEhJKnDMxMdFznX379pXnlgEAAAAAqDMIlFClDMPQlClTdOeddyopKUmtWrXSiBEj9Pjjj6tdu3basGGD7r//fr388svVXsurr76qM2fOVOjc+Ph4WSwWSZLD4ajKsgAAAAAA8Hl+3i4AtcuMGTO0cOFCtW3bVkuWLFFkZGSh4zk5OXrzzTeVmZlZrXVERkYqLS1Ns2fP1osvvmjq3B9++EEpKSnq3bu3Dh48qBUrVujFF19UUFBQNVULAAAAAIBv4QklVJnU1FS99tprCgkJUXJycpEwSZKCgoL05JNPavLkydVaS2xsrKKiovTWW2/p2LFjps4teCIpJiZG0dHROnfunNasWVMdZQIAAAAA4JMIlFBlli5dKpfLpREjRig0NLTUsQEBAdVai5+fn5555hnl5uaaekLJ5XJ59k/q1auXoqOjZbFYFB8fX43VAgAAAADgW1jyhiqze/duSVLXrl1Nn7tmzRodOHCg2GNff/11herp37+/5s+fr2XLlmn06NH6/e9/X+Y5GzZs0I8//qgRI0YoICBALVu2VKdOnZSSkqLU1FRFRUWVa2634ZJhuCpUd11jGEahP1E2emYePTOPnlVMTe6bYbjkdDq9XUYReXl5hf6sjQIDA71dAgAAVY5ACVXm9OnTkqTw8HDT565du1Zr166t0nosFoumTZume++9V88//7yWL19e5jkFTyLFxMR4PouJiVFKSoocDoeeffbZcs09d/zdchv5FSscAIBqYNjcppeBX0rp6eneLqFa2Gy2cv+FFAAAvoRACTXCokWLNGDAgGKPjRo1SomJiRW6bteuXXX33Xfr448/1o4dO3THHXeUODY9PV0bNmxQVFSUbrvtNs/n/fv318SJE5WYmKinn35aNputzHlDc1fKYlysUM11jeE2lJubq4CAAFktrMItD3pmHj0zj55VTE3um7PpowpueKW3yygiLy9P6enpCgsLk7+/v7fLAQAA5USghCoTGhqqAwcO6OTJk7r66qu9XY7Hc889p82bN+u5557Tpk2bShyXmJio/Px8RUdHF/q8YcOG6tOnj5KTk7Vx40b17NmzzDmtNqssNewXiRrrvysDrRarrDZ6Vi70zDx6Zh49q5ga3DerzVajl175+/vX6PoAAEBhNesnHfi0jh07SpK2bdvm5UoKa9u2rQYOHKjPP/9cq1evLnFcwdvd4uLiZLfbC30lJydLEptzAwAAAAAgnlBCFYqNjdW8efO0ePFijRo1Sk2aNClxbMFygEvl6aef1urVq/XCCy8U2h+pQEpKig4dOqTIyMgSl8V9+OGH+uijj/TTTz+padOm1V0yAAAAAAA1FoESqkxUVJSeeuopzZ07Vw8++KAWL16sVq1aFRrjdDr11ltvKSMjQ88999wlq61ly5Z65JFHtHDhQi1durTI8YInj8aPH6+hQ4cWe43p06dr7ty5SkpK0pgxY6q1XgAAAAAAajICJVSpqVOnyul0auHCherQoYO6du2qa6+9VvXq1dORI0e0ZcsWZWZmaurUqZe8tgkTJsjhcCgtLa3Q5+fOndOaNWtUv3599e/fv8TzY2NjNXfuXMXHxxMoAQAAAADqNPZQQpWyWq166aWX9Mknnyg6OlppaWlatGiRFi5cqM8++0zdu3fX6tWrNWHChEteW0hIiMaOHVvk85UrVyo7O1v33nuvGjRoUOL5rVu3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6b///a/27NmjvHnzqkqVKjIajQoJCdGQIUN06dKlZPueMmWKunXrppMnT6p8+fLKmTOnfvvtN7355puaN29ekvanTp1SQECAVqxYoatXr8rDw0Ply5fX9evXtWrVKjVp0kQ//fRTkuMOHz4sPz8/ff3117p48aLKlSunSpUqKT4+Xnv27NHEiRN1+fJlq3NjbfzSgw+1ffr00S+//KI8efLoueee019//aWuXbtm6DC75O6PXbt2qX79+po/f74iIyNVsWJFubu76+DBgxozZoyaN2+uqKioRMc0bNhQ0oMC0MOuX7+uo0ePSpKuXr2apLhnbv/CCy/I2dk5UVwffPCB2rZtq3Xr1ikmJkZeXl7KmTOntm3bpu7du1uevkvpulK7P5/Uo3m7c+eOOnXqpAULFujixYsqVqyYKlasqJiYGAUFBalVq1b66quvUu0zKChILVq00LZt21SiRAmVL19eBoMhxfZOTk6qW7euihYtKunB/F5169a1fNWqVUuS9MYbb0iSli9fLqPRmGxf27dvV2RkpIoUKaJXXnklrWl4LKPRqE6dOmnUqFGKjY1VhQoVFBsbq59//lktW7ZMtgB57949derUSePGjdNff/2lYsWKqWTJkgoODlbTpk3166+/pni+e/fuKSAgQAEBAfr555+VkJAgLy8v3b9/Xxs3blTr1q01c+bMRMeMGTNGtWvXVmRkpAIDAxPtM5lMeuedd3TlyhU1adIkyX4AAIDkUFACkC2YP7A7ODiofPnyNuv3l19+0c6dO7VmzRr98ccf2rZtm06cOKGSJUsqJiZGXbp0UVhYmCpXrqyQkBBLmz///FNhYWH68MMPlTdv3iT9Xrp0SV988YXmz5+vsLAwhYSE6PTp03rrrbckSePHj9etW7cSHVOkSBHNnTtXp0+f1okTJxQaGqq9e/fq9OnTmjp1qoxGo/r376+7d+8mOm7KlCm6deuWOnfurLCwMO3bt08hISE6ceKEwsLCNHXqVOXPn9+qvKQn/uDgYM2YMUMGg0GTJ0/WiRMntG3bNoWFhWnMmDEaM2aMVTGkldFotDyxUaFCBUkPij5vvPGGbt68qRYtWuivv/5SaGioDhw4oJCQEJUqVUpHjhzRgAEDEvXl6+srKWlBaefOnTKZTCpZsmSy+83fm483mzFjhubNm6eSJUtq5cqVioiIUGhoqMLC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
"/>

As we can see above, our expectation that sales tax does not change the PPP Index significantly was right.

# 4. Displaying the currencies for each country and showing the price differences

Our next objective is to display each country's currencies by symbol and code. To achieve this, we imported a CSV file that contains information about country names and their respective codes. We then selected specific columns from the imported file, relabeled column names for clarity, and joined them with our latte table to get the currency code column. After that, an essential step in our process was using a function that gave us the exchange rates for every currency code. We saved the exchange rates into an array variable so we could use it to multiply each price and get a local currency for every country. Next, we wanted to know the difference between the latte prices in Canada and other countries. Therefore, we subtracted the price of a Canadian latte from that of a converted to CAD foreign latte.

Below is the table that we have created.

<table border="1" class="dataframe">
<thead>
<tr>
<th>Country</th> <th>Currency</th> <th>Currency Code</th> <th>Latte Price In Local Currency</th> <th>Latte Price (CAD)</th> <th>Sales Tax</th> <th>Price Difference (CAD)</th> <th>Purchasing Power Parity</th> <th>Purchasing Power Parity With Tax</th>
</tr>
</thead>
<tbody>
<tr>
<td>ANDORRA       </td> <td>Euro             </td> <td>EUR          </td> <td>3.16                         </td> <td>4.73             </td> <td>0.045    </td> <td>-0.82                 </td> <td>0.851948               </td> <td>0.852252                        </td>
</tr>
<tr>
<td>ARGENTINA     </td> <td>Argentine Peso   </td> <td>ARS          </td> <td>4767.62                      </td> <td>6.74             </td> <td>0.21     </td> <td>1.19                  </td> <td>1.21299                </td> <td>1.21441                         </td>
</tr>
<tr>
<td>AUSTRALIA     </td> <td>Australian Dollar</td> <td>AUD          </td> <td>6.37                         </td> <td>5.73             </td> <td>0.1      </td> <td>0.18                  </td> <td>1.03117                </td> <td>1.03243                         </td>
</tr>
<tr>
<td>AUSTRIA       </td> <td>Euro             </td> <td>EUR          </td> <td>3.35                         </td> <td>5.02             </td> <td>0.2      </td> <td>-0.53                 </td> <td>0.903896               </td> <td>0.904505                        </td>
</tr>
<tr>
<td>AZERBAIJAN    </td> <td>Azerbaijan Manat </td> <td>AZN          </td> <td>5.8                          </td> <td>4.92             </td> <td>0.18     </td> <td>-0.63                 </td> <td>0.885714               </td> <td>0.886486                        </td>
</tr>
<tr>
<td>BAHAMAS       </td> <td>Bahamian Dollar  </td> <td>BSD          </td> <td>3.75                         </td> <td>5.41             </td> <td>0.12     </td> <td>-0.14                 </td> <td>0.974026               </td> <td>0.974775                        </td>
</tr>
<tr>
<td>BAHRAIN       </td> <td>Bahraini Dinar   </td> <td>BHD          </td> <td>1.59                         </td> <td>6.12             </td> <td>0.1      </td> <td>0.57                  </td> <td>1.1013                 </td> <td>1.1027                          </td>
</tr>
<tr>
<td>BELGIUM       </td> <td>Euro             </td> <td>EUR          </td> <td>3.39                         </td> <td>5.08             </td> <td>0.21     </td> <td>-0.47                 </td> <td>0.914286               </td> <td>0.915315                        </td>
</tr>
<tr>
<td>BOLIVIA       </td> <td>Boliviano        </td> <td>BOB          </td> <td>22.06                        </td> <td>4.6              </td> <td>0.13     </td> <td>-0.95                 </td> <td>0.828571               </td> <td>0.828829                        </td>
</tr>
<tr>
<td>BRAZIL        </td> <td>Brazilian Real   </td> <td>BRL          </td> <td>12.31                        </td> <td>2.83             </td> <td>0.22     </td> <td>-2.72                 </td> <td>0.509091               </td> <td>0.50991                         </td>
</tr>
<tr>
<td>BULGARIA      </td> <td>Bulgarian Lev    </td> <td>BGN          </td> <td>5.04                         </td> <td>3.88             </td> <td>0.2      </td> <td>-1.67                 </td> <td>0.698701               </td> <td>0.699099                        </td>
</tr>
<tr>
<td>CAMBODIA      </td> <td>Riel             </td> <td>KHR          </td> <td>13036                        </td> <td>4.69             </td> <td>0.1      </td> <td>-0.86                 </td> <td>0.844156               </td> <td>0.845045                        </td>
</tr>
<tr>
<td>CANADA        </td> <td>Canadian Dollar  </td> <td>CAD          </td> <td>5.55                         </td> <td>5.55             </td> <td>0.109981 </td> <td>0                     </td> <td>1                      </td> <td>1                               </td>
</tr>
<tr>
<td>CHILE         </td> <td>Chilean Peso     </td> <td>CLP          </td> <td>4925.2                       </td> <td>7.14             </td> <td>0.19     </td> <td>1.59                  </td> <td>1.28571                </td> <td>1.28649                         </td>
</tr>
<tr>
<td>CHINA         </td> <td>Yuan Renminbi    </td> <td>CNY          </td> <td>30.88                        </td> <td>6.1              </td> <td>0.13     </td> <td>0.55                  </td> <td>1.0987                 </td> <td>1.0991                          </td>
</tr>
<tr>
<td>COLOMBIA      </td> <td>Colombian Peso   </td> <td>COP          </td> <td>10970.5                      </td> <td>3.61             </td> <td>0.19     </td> <td>-1.94                 </td> <td>0.649351               </td> <td>0.65045                         </td>
</tr>
<tr>
<td>COSTA RICA    </td> <td>Costa Rican Colon</td> <td>CRC          </td> <td>2134.51                      </td> <td>6.09             </td> <td>0.13     </td> <td>0.54                  </td> <td>1.0961                 </td> <td>1.0973                          </td>
</tr>
<tr>
<td>CYPRUS        </td> <td>Euro             </td> <td>EUR          </td> <td>2.86                         </td> <td>4.28             </td> <td>0.19     </td> <td>-1.27                 </td> <td>0.771429               </td> <td>0.771171                        </td>
</tr>
<tr>
<td>CZECH REPUBLIC</td> <td>Czech Koruna     </td> <td>CZK          </td> <td>95.01                        </td> <td>5.67             </td> <td>0.21     </td> <td>0.12                  </td> <td>1.02078                </td> <td>1.02162                         </td>
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
                #map_c17e37e604c3b657fc50d03d75d3614e {
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
    
    
            &lt;div class="folium-map" id="map_c17e37e604c3b657fc50d03d75d3614e" &gt;&lt;/div&gt;
        
&lt;/body&gt;
&lt;script&gt;
    
    
            var map_c17e37e604c3b657fc50d03d75d3614e = L.map(
                "map_c17e37e604c3b657fc50d03d75d3614e",
                {
                    center: [7.783333330000001, 32.525],
                    crs: L.CRS.EPSG3857,
                    ...{
  "zoom": 1,
  "zoomControl": true,
  "preferCanvas": false,
  "clusteredMarker": false,
  "includeColorScaleOutliers": true,
  "radiusInMeters": false,
}

                }
            );

            

        
    
            var tile_layer_1a3bb086e632b5e6be2d68782f6ce502 = L.tileLayer(
                "https://tile.openstreetmap.org/{z}/{x}/{y}.png",
                {
  "minZoom": -1,
  "maxZoom": 17,
  "maxNativeZoom": 17,
  "noWrap": false,
  "attribution": "\u0026copy; \u003ca href=\"https://www.openstreetmap.org/copyright\"\u003eOpenStreetMap\u003c/a\u003e contributors",
  "subdomains": "abc",
  "detectRetina": false,
  "tms": false,
  "opacity": 1,
}

            );
        
    
            tile_layer_1a3bb086e632b5e6be2d68782f6ce502.addTo(map_c17e37e604c3b657fc50d03d75d3614e);
        
    
            var marker_ea245e9a1e8d0975900278463974d880 = L.marker(
                [42.5, 1.516667],
                {
}
            ).addTo(map_c17e37e604c3b657fc50d03d75d3614e);
        
    
            var icon_0dedc4b3133f5c21c6a1dc7580cc477f = L.AwesomeMarkers.icon(
                {
  "markerColor": "red",
  "iconColor": "white",
  "icon": "sign-blank",
  "prefix": "glyphicon",
  "extraClasses": "fa-rotate-0",
}
            );
            marker_ea245e9a1e8d0975900278463974d880.setIcon(icon_0dedc4b3133f5c21c6a1dc7580cc477f);
        
    
        var popup_0f124fa6b92becb8b3c361a57f439367 = L.popup({
  "maxWidth": "100%",
});

        
            
                var html_6b477066b2f0a2a6be5bc9532f2fe52e = $(`&lt;div id="html_6b477066b2f0a2a6be5bc9532f2fe52e" style="width: 100.0%; height: 100.0%;"&gt;EUR&lt;/div&gt;`)[0];
                popup_0f124fa6b92becb8b3c361a57f439367.setContent(html_6b477066b2f0a2a6be5bc9532f2fe52e);
            
        

        marker_ea245e9a1e8d0975900278463974d880.bindPopup(popup_0f124fa6b92becb8b3c361a57f439367)
        ;

        
    
    
            var marker_a925bcf58da9fa76a480ea1450dd7866 = L.marker(
                [-34.58333333, -58.666667],
                {
}
            ).addTo(map_c17e37e604c3b657fc50d03d75d3614e);
        
    
            var icon_9d7f0e24d464afbb8f96c12583a14c6a = L.AwesomeMarkers.icon(
                {
  "markerColor": "orange",
  "iconColor": "white",
  "icon": "sign-blank",
  "prefix": "glyphicon",
  "extraClasses": "fa-rotate-0",
}
            );
            marker_a925bcf58da9fa76a480ea1450dd7866.setIcon(icon_9d7f0e24d464afbb8f96c12583a14c6a);
        
    
        var popup_d0094a6b78829303dd26cef490e21d2a = L.popup({
  "maxWidth": "100%",
});

        
            
                var html_69c953130096f6722ba1df590d29d661 = $(`&lt;div id="html_69c953130096f6722ba1df590d29d661" style="width: 100.0%; height: 100.0%;"&gt;ARS&lt;/div&gt;`)[0];
                popup_d0094a6b78829303dd26cef490e21d2a.setContent(html_69c953130096f6722ba1df590d29d661);
            
        

        marker_a925bcf58da9fa76a480ea1450dd7866.bindPopup(popup_d0094a6b78829303dd26cef490e21d2a)
        ;

        
    
    
            var marker_54454ba27978d0de07af1e0efb4e9296 = L.marker(
                [-35.26666667, 149.133333],
                {
}
            ).addTo(map_c17e37e604c3b657fc50d03d75d3614e);
        
    
            var icon_7d48ea82e1c4abe7288693a9c3f9c95d = L.AwesomeMarkers.icon(
                {
  "markerColor": "purple",
  "iconColor": "white",
  "icon": "sign-blank",
  "prefix": "glyphicon",
  "extraClasses": "fa-rotate-0",
}
            );
            marker_54454ba27978d0de07af1e0efb4e9296.setIcon(icon_7d48ea82e1c4abe7288693a9c3f9c95d);
        
    
        var popup_93578d183ac06ce69c2911d10c773545 = L.popup({
  "maxWidth": "100%",
});

        
            
                var html_61688fa7a99e196ba98324dd423c3b71 = $(`&lt;div id="html_61688fa7a99e196ba98324dd423c3b71" style="width: 100.0%; height: 100.0%;"&gt;AUD&lt;/div&gt;`)[0];
                popup_93578d183ac06ce69c2911d10c773545.setContent(html_61688fa7a99e196ba98324dd423c3b71);
            
        

        marker_54454ba27978d0de07af1e0efb4e9296.bindPopup(popup_93578d183ac06ce69c2911d10c773545)
        ;

        
    
    
            var marker_2729a42fb983d20dabbc7f67a28eb889 = L.marker(
                [48.2, 16.366667],
                {
}
            ).addTo(map_c17e37e604c3b657fc50d03d75d3614e);
        
    
            var icon_90016c663b16e65226a349e26ff6d133 = L.AwesomeMarkers.icon(
                {
  "markerColor": "red",
  "iconColor": "white",
  "icon": "sign-blank",
  "prefix": "glyphicon",
  "extraClasses": "fa-rotate-0",
}
            );
            marker_2729a42fb983d20dabbc7f67a28eb889.setIcon(icon_90016c663b16e65226a349e26ff6d133);
        
    
        var popup_bb1667a8e00849583f6d46822b1e72f4 = L.popup({
  "maxWidth": "100%",
});

        
            
                var html_29bc229d7431c2a5a4a1f0f069f4398a = $(`&lt;div id="html_29bc229d7431c2a5a4a1f0f069f4398a" style="width: 100.0%; height: 100.0%;"&gt;EUR&lt;/div&gt;`)[0];
                popup_bb1667a8e00849583f6d46822b1e72f4.setContent(html_29bc229d7431c2a5a4a1f0f069f4398a);
            
        

        marker_2729a42fb983d20dabbc7f67a28eb889.bindPopup(popup_bb1667a8e00849583f6d46822b1e72f4)
        ;

        
    
    
            var marker_6361a5069ad832151b911737fe1895b7 = L.marker(
                [40.38333333, 49.866667],
                {
}
            ).addTo(map_c17e37e604c3b657fc50d03d75d3614e);
        
    
            var icon_d7937159273a76a3b80f289715ac8f00 = L.AwesomeMarkers.icon(
                {
  "markerColor": "red",
  "iconColor": "white",
  "icon": "sign-blank",
  "prefix": "glyphicon",
  "extraClasses": "fa-rotate-0",
}
            );
            marker_6361a5069ad832151b911737fe1895b7.setIcon(icon_d7937159273a76a3b80f289715ac8f00);
        
    
        var popup_cf32ee7381c0426fd99934427ad0e5ad = L.popup({
  "maxWidth": "100%",
});

        
            
                var html_e057879f10f2032338e87c490f7babff = $(`&lt;div id="html_e057879f10f2032338e87c490f7babff" style="width: 100.0%; height: 100.0%;"&gt;AZN&lt;/div&gt;`)[0];
                popup_cf32ee7381c0426fd99934427ad0e5ad.setContent(html_e057879f10f2032338e87c490f7babff);
            
        

        marker_6361a5069ad832151b911737fe1895b7.bindPopup(popup_cf32ee7381c0426fd99934427ad0e5ad)
        ;

        
    
    
            var marker_07b00e1bd0e9e238df279cad1d7f519d = L.marker(
                [25.08333333, -77.35],
                {
}
            ).addTo(map_c17e37e604c3b657fc50d03d75d3614e);
        
    
            var icon_669c95f14f95f363a42a82efea01041f = L.AwesomeMarkers.icon(
                {
  "markerColor": "blue",
  "iconColor": "white",
  "icon": "sign-blank",
  "prefix": "glyphicon",
  "extraClasses": "fa-rotate-0",
}
            );
            marker_07b00e1bd0e9e238df279cad1d7f519d.setIcon(icon_669c95f14f95f363a42a82efea01041f);
        
    
        var popup_87dee38ee06d184971af3e6c04b2a28e = L.popup({
  "maxWidth": "100%",
});

        
            
                var html_0bea5cd595cfcbda4971308c4605cfaf = $(`&lt;div id="html_0bea5cd595cfcbda4971308c4605cfaf" style="width: 100.0%; height: 100.0%;"&gt;BSD&lt;/div&gt;`)[0];
                popup_87dee38ee06d184971af3e6c04b2a28e.setContent(html_0bea5cd595cfcbda4971308c4605cfaf);
            
        

        marker_07b00e1bd0e9e238df279cad1d7f519d.bindPopup(popup_87dee38ee06d184971af3e6c04b2a28e)
        ;

        
    
    
            var marker_df2cb2643d4a75b5cc512b9afe229970 = L.marker(
                [26.23333333, 50.566667],
                {
}
            ).addTo(map_c17e37e604c3b657fc50d03d75d3614e);
        
    
            var icon_d4f9b0f27a616fc714bd47abb0685f3b = L.AwesomeMarkers.icon(
                {
  "markerColor": "green",
  "iconColor": "white",
  "icon": "sign-blank",
  "prefix": "glyphicon",
  "extraClasses": "fa-rotate-0",
}
            );
            marker_df2cb2643d4a75b5cc512b9afe229970.setIcon(icon_d4f9b0f27a616fc714bd47abb0685f3b);
        
    
        var popup_7c2a0df31734cdabf59578fd8d24c3d0 = L.popup({
  "maxWidth": "100%",
});

        
            
                var html_4f5b799e7b5908178c41974a26dda98c = $(`&lt;div id="html_4f5b799e7b5908178c41974a26dda98c" style="width: 100.0%; height: 100.0%;"&gt;BHD&lt;/div&gt;`)[0];
                popup_7c2a0df31734cdabf59578fd8d24c3d0.setContent(html_4f5b799e7b5908178c41974a26dda98c);
            
        

        marker_df2cb2643d4a75b5cc512b9afe229970.bindPopup(popup_7c2a0df31734cdabf59578fd8d24c3d0)
        ;

        
    
    
            var marker_b09b0cbc370a7d70bd898631cba027de = L.marker(
                [50.83333333, 4.333333],
                {
}
            ).addTo(map_c17e37e604c3b657fc50d03d75d3614e);
        
    
            var icon_89e3a9ef842fcd3776379e68a36e643e = L.AwesomeMarkers.icon(
                {
  "markerColor": "red",
  "iconColor": "white",
  "icon": "sign-blank",
  "prefix": "glyphicon",
  "extraClasses": "fa-rotate-0",
}
            );
            marker_b09b0cbc370a7d70bd898631cba027de.setIcon(icon_89e3a9ef842fcd3776379e68a36e643e);
        
    
        var popup_1a35d13d931f0576b1f93b236e95128e = L.popup({
  "maxWidth": "100%",
});

        
            
                var html_7f6ded973d2d1179f92ca98562faa212 = $(`&lt;div id="html_7f6ded973d2d1179f92ca98562faa212" style="width: 100.0%; height: 100.0%;"&gt;EUR&lt;/div&gt;`)[0];
                popup_1a35d13d931f0576b1f93b236e95128e.setContent(html_7f6ded973d2d1179f92ca98562faa212);
            
        

        marker_b09b0cbc370a7d70bd898631cba027de.bindPopup(popup_1a35d13d931f0576b1f93b236e95128e)
        ;

        
    
    
            var marker_bfad5577e93aa01144cbe4baa3056119 = L.marker(
                [-16.5, -68.15],
                {
}
            ).addTo(map_c17e37e604c3b657fc50d03d75d3614e);
        
    
            var icon_3cfc00a5bb299975e7d1e5288af7f633 = L.AwesomeMarkers.icon(
                {
  "markerColor": "orange",
  "iconColor": "white",
  "icon": "sign-blank",
  "prefix": "glyphicon",
  "extraClasses": "fa-rotate-0",
}
            );
            marker_bfad5577e93aa01144cbe4baa3056119.setIcon(icon_3cfc00a5bb299975e7d1e5288af7f633);
        
    
        var popup_d46a2f1bac5d89e2c9741b08b8f015e4 = L.popup({
  "maxWidth": "100%",
});

        
            
                var html_d5a860d181b470996f2215f9b9def7c6 = $(`&lt;div id="html_d5a860d181b470996f2215f9b9def7c6" style="width: 100.0%; height: 100.0%;"&gt;BOB&lt;/div&gt;`)[0];
                popup_d46a2f1bac5d89e2c9741b08b8f015e4.setContent(html_d5a860d181b470996f2215f9b9def7c6);
            
        

        marker_bfad5577e93aa01144cbe4baa3056119.bindPopup(popup_d46a2f1bac5d89e2c9741b08b8f015e4)
        ;

        
    
    
            var marker_5271c32609ea2c0c22815167c3655ceb = L.marker(
                [-15.78333333, -47.916667],
                {
}
            ).addTo(map_c17e37e604c3b657fc50d03d75d3614e);
        
    
            var icon_d67685688021fd44977ddbf0be0ef5da = L.AwesomeMarkers.icon(
                {
  "markerColor": "orange",
  "iconColor": "white",
  "icon": "sign-blank",
  "prefix": "glyphicon",
  "extraClasses": "fa-rotate-0",
}
            );
            marker_5271c32609ea2c0c22815167c3655ceb.setIcon(icon_d67685688021fd44977ddbf0be0ef5da);
        
    
        var popup_6d9f68c4e6df991955152ded54099df6 = L.popup({
  "maxWidth": "100%",
});

        
            
                var html_7a7aa5badb01cc6344b4bdb9c9f13b78 = $(`&lt;div id="html_7a7aa5badb01cc6344b4bdb9c9f13b78" style="width: 100.0%; height: 100.0%;"&gt;BRL&lt;/div&gt;`)[0];
                popup_6d9f68c4e6df991955152ded54099df6.setContent(html_7a7aa5badb01cc6344b4bdb9c9f13b78);
            
        

        marker_5271c32609ea2c0c22815167c3655ceb.bindPopup(popup_6d9f68c4e6df991955152ded54099df6)
        ;

        
    
    
            var marker_5a9ff3a3eae9206b43470eb10ee0ec59 = L.marker(
                [42.68333333, 23.316667],
                {
}
            ).addTo(map_c17e37e604c3b657fc50d03d75d3614e);
        
    
            var icon_41620579e23b48f8b01c9c2bbf28b471 = L.AwesomeMarkers.icon(
                {
  "markerColor": "red",
  "iconColor": "white",
  "icon": "sign-blank",
  "prefix": "glyphicon",
  "extraClasses": "fa-rotate-0",
}
            );
            marker_5a9ff3a3eae9206b43470eb10ee0ec59.setIcon(icon_41620579e23b48f8b01c9c2bbf28b471);
        
    
        var popup_9d16d58155a0075485661bbe147e88a9 = L.popup({
  "maxWidth": "100%",
});

        
            
                var html_054a6b4f54aeb3cd498201f868c6f08f = $(`&lt;div id="html_054a6b4f54aeb3cd498201f868c6f08f" style="width: 100.0%; height: 100.0%;"&gt;BGN&lt;/div&gt;`)[0];
                popup_9d16d58155a0075485661bbe147e88a9.setContent(html_054a6b4f54aeb3cd498201f868c6f08f);
            
        

        marker_5a9ff3a3eae9206b43470eb10ee0ec59.bindPopup(popup_9d16d58155a0075485661bbe147e88a9)
        ;

        
    
    
            var marker_050bdc8796d2e832c1299ed0706c71e6 = L.marker(
                [11.55, 104.916667],
                {
}
            ).addTo(map_c17e37e604c3b657fc50d03d75d3614e);
        
    
            var icon_b2f6414a66c713bc97476660d5d9dcd6 = L.AwesomeMarkers.icon(
                {
  "markerColor": "green",
  "iconColor": "white",
  "icon": "sign-blank",
  "prefix": "glyphicon",
  "extraClasses": "fa-rotate-0",
}
            );
            marker_050bdc8796d2e832c1299ed0706c71e6.setIcon(icon_b2f6414a66c713bc97476660d5d9dcd6);
        
    
        var popup_972b0cb09cd2f90f262a098f3dd0e7bd = L.popup({
  "maxWidth": "100%",
});

        
            
                var html_030c25b9743e638b1c39017c09acb5c5 = $(`&lt;div id="html_030c25b9743e638b1c39017c09acb5c5" style="width: 100.0%; height: 100.0%;"&gt;KHR&lt;/div&gt;`)[0];
                popup_972b0cb09cd2f90f262a098f3dd0e7bd.setContent(html_030c25b9743e638b1c39017c09acb5c5);
            
        

        marker_050bdc8796d2e832c1299ed0706c71e6.bindPopup(popup_972b0cb09cd2f90f262a098f3dd0e7bd)
        ;

        
    
    
            var marker_100eb1824a5a7ef477c5b178f8928340 = L.marker(
                [45.41666667, -75.7],
                {
}
            ).addTo(map_c17e37e604c3b657fc50d03d75d3614e);
        
    
            var icon_c0e41164e35ced7040bc3f6c4e39baf8 = L.AwesomeMarkers.icon(
                {
  "markerColor": "blue",
  "iconColor": "white",
  "icon": "sign-blank",
  "prefix": "glyphicon",
  "extraClasses": "fa-rotate-0",
}
            );
            marker_100eb1824a5a7ef477c5b178f8928340.setIcon(icon_c0e41164e35ced7040bc3f6c4e39baf8);
        
    
        var popup_191dc9c8830378b1e61ba12573c44600 = L.popup({
  "maxWidth": "100%",
});

        
            
                var html_b69cfffc7cd40caf58bb1f7c4c00b68b = $(`&lt;div id="html_b69cfffc7cd40caf58bb1f7c4c00b68b" style="width: 100.0%; height: 100.0%;"&gt;CAD&lt;/div&gt;`)[0];
                popup_191dc9c8830378b1e61ba12573c44600.setContent(html_b69cfffc7cd40caf58bb1f7c4c00b68b);
            
        

        marker_100eb1824a5a7ef477c5b178f8928340.bindPopup(popup_191dc9c8830378b1e61ba12573c44600)
        ;

        
    
    
            var marker_2064e306ff9a25bb0540de53bc37770d = L.marker(
                [-33.45, -70.666667],
                {
}
            ).addTo(map_c17e37e604c3b657fc50d03d75d3614e);
        
    
            var icon_1de92f2c04032434857058964d01dc77 = L.AwesomeMarkers.icon(
                {
  "markerColor": "orange",
  "iconColor": "white",
  "icon": "sign-blank",
  "prefix": "glyphicon",
  "extraClasses": "fa-rotate-0",
}
            );
            marker_2064e306ff9a25bb0540de53bc37770d.setIcon(icon_1de92f2c04032434857058964d01dc77);
        
    
        var popup_0104f474a08e44b36f95d8f01ea703e5 = L.popup({
  "maxWidth": "100%",
});

        
            
                var html_a2ef150ae00b0a373e2c8994d6ed4554 = $(`&lt;div id="html_a2ef150ae00b0a373e2c8994d6ed4554" style="width: 100.0%; height: 100.0%;"&gt;CLP&lt;/div&gt;`)[0];
                popup_0104f474a08e44b36f95d8f01ea703e5.setContent(html_a2ef150ae00b0a373e2c8994d6ed4554);
            
        

        marker_2064e306ff9a25bb0540de53bc37770d.bindPopup(popup_0104f474a08e44b36f95d8f01ea703e5)
        ;

        
    
    
            var marker_fdfd58ee82131a033c309fce663b7fc3 = L.marker(
                [39.91666667, 116.383333],
                {
}
            ).addTo(map_c17e37e604c3b657fc50d03d75d3614e);
        
    
            var icon_2a84aa468148b191e31369386308a34a = L.AwesomeMarkers.icon(
                {
  "markerColor": "green",
  "iconColor": "white",
  "icon": "sign-blank",
  "prefix": "glyphicon",
  "extraClasses": "fa-rotate-0",
}
            );
            marker_fdfd58ee82131a033c309fce663b7fc3.setIcon(icon_2a84aa468148b191e31369386308a34a);
        
    
        var popup_29cc2af430591e0bedc8ae93ae4a3be5 = L.popup({
  "maxWidth": "100%",
});

        
            
                var html_5a8bfd0c96e724aa0facdbea208df70d = $(`&lt;div id="html_5a8bfd0c96e724aa0facdbea208df70d" style="width: 100.0%; height: 100.0%;"&gt;CNY&lt;/div&gt;`)[0];
                popup_29cc2af430591e0bedc8ae93ae4a3be5.setContent(html_5a8bfd0c96e724aa0facdbea208df70d);
            
        

        marker_fdfd58ee82131a033c309fce663b7fc3.bindPopup(popup_29cc2af430591e0bedc8ae93ae4a3be5)
        ;

        
    
    
            var marker_82b4318cd482e47d66cf33096856df03 = L.marker(
                [4.6, -74.083333],
                {
}
            ).addTo(map_c17e37e604c3b657fc50d03d75d3614e);
        
    
            var icon_ba9b47ae966aae87ce21d2854967cad9 = L.AwesomeMarkers.icon(
                {
  "markerColor": "orange",
  "iconColor": "white",
  "icon": "sign-blank",
  "prefix": "glyphicon",
  "extraClasses": "fa-rotate-0",
}
            );
            marker_82b4318cd482e47d66cf33096856df03.setIcon(icon_ba9b47ae966aae87ce21d2854967cad9);
        
    
        var popup_361ce5e2255e2640fab7f7c99366debb = L.popup({
  "maxWidth": "100%",
});

        
            
                var html_f2b971e85ff5e2a60e762e9922687da8 = $(`&lt;div id="html_f2b971e85ff5e2a60e762e9922687da8" style="width: 100.0%; height: 100.0%;"&gt;COP&lt;/div&gt;`)[0];
                popup_361ce5e2255e2640fab7f7c99366debb.setContent(html_f2b971e85ff5e2a60e762e9922687da8);
            
        

        marker_82b4318cd482e47d66cf33096856df03.bindPopup(popup_361ce5e2255e2640fab7f7c99366debb)
        ;

        
    
    
            var marker_b01a17bbb8a421392c2baf50db96b0e1 = L.marker(
                [9.933333333, -84.083333],
                {
}
            ).addTo(map_c17e37e604c3b657fc50d03d75d3614e);
        
    
            var icon_b6a0e125fc61f52ac88fd758ad5ec2b3 = L.AwesomeMarkers.icon(
                {
  "markerColor": "black",
  "iconColor": "white",
  "icon": "sign-blank",
  "prefix": "glyphicon",
  "extraClasses": "fa-rotate-0",
}
            );
            marker_b01a17bbb8a421392c2baf50db96b0e1.setIcon(icon_b6a0e125fc61f52ac88fd758ad5ec2b3);
        
    
        var popup_b8fb082a64873af5cda4f93510634e03 = L.popup({
  "maxWidth": "100%",
});

        
            
                var html_f66753c5e1a86968e0172a5cf241a6fb = $(`&lt;div id="html_f66753c5e1a86968e0172a5cf241a6fb" style="width: 100.0%; height: 100.0%;"&gt;CRC&lt;/div&gt;`)[0];
                popup_b8fb082a64873af5cda4f93510634e03.setContent(html_f66753c5e1a86968e0172a5cf241a6fb);
            
        

        marker_b01a17bbb8a421392c2baf50db96b0e1.bindPopup(popup_b8fb082a64873af5cda4f93510634e03)
        ;

        
    
    
            var marker_2b89e7c193f620a90be80216e1eb4191 = L.marker(
                [35.16666667, 33.366667],
                {
}
            ).addTo(map_c17e37e604c3b657fc50d03d75d3614e);
        
    
            var icon_9399a68ee16e7874c6f7e22d922fdd77 = L.AwesomeMarkers.icon(
                {
  "markerColor": "red",
  "iconColor": "white",
  "icon": "sign-blank",
  "prefix": "glyphicon",
  "extraClasses": "fa-rotate-0",
}
            );
            marker_2b89e7c193f620a90be80216e1eb4191.setIcon(icon_9399a68ee16e7874c6f7e22d922fdd77);
        
    
        var popup_8d97ebc553b75f9455ef399a244beb83 = L.popup({
  "maxWidth": "100%",
});

        
            
                var html_5c78284ece27b9a55fd463383ad16745 = $(`&lt;div id="html_5c78284ece27b9a55fd463383ad16745" style="width: 100.0%; height: 100.0%;"&gt;EUR&lt;/div&gt;`)[0];
                popup_8d97ebc553b75f9455ef399a244beb83.setContent(html_5c78284ece27b9a55fd463383ad16745);
            
        

        marker_2b89e7c193f620a90be80216e1eb4191.bindPopup(popup_8d97ebc553b75f9455ef399a244beb83)
        ;

        
    
    
            var marker_298c876ee50281aaa6d41e9e309aecdd = L.marker(
                [50.08333333, 14.466667],
                {
}
            ).addTo(map_c17e37e604c3b657fc50d03d75d3614e);
        
    
            var icon_af9943e18d80b51119ae380b3771463f = L.AwesomeMarkers.icon(
                {
  "markerColor": "red",
  "iconColor": "white",
  "icon": "sign-blank",
  "prefix": "glyphicon",
  "extraClasses": "fa-rotate-0",
}
            );
            marker_298c876ee50281aaa6d41e9e309aecdd.setIcon(icon_af9943e18d80b51119ae380b3771463f);
        
    
        var popup_81aea535398956895b162903d5908df3 = L.popup({
  "maxWidth": "100%",
});

        
            
                var html_ca27c2847cb0b81e9000f47fc9a2d32f = $(`&lt;div id="html_ca27c2847cb0b81e9000f47fc9a2d32f" style="width: 100.0%; height: 100.0%;"&gt;CZK&lt;/div&gt;`)[0];
                popup_81aea535398956895b162903d5908df3.setContent(html_ca27c2847cb0b81e9000f47fc9a2d32f);
            
        

        marker_298c876ee50281aaa6d41e9e309aecdd.bindPopup(popup_81aea535398956895b162903d5908df3)
        ;

        
    
&lt;/script&gt;
&lt;/html&gt;' style="position:absolute;width:100%;height:100%;left:0;top:0;border:none !important;" webkitallowfullscreen=""></iframe></div></div>
