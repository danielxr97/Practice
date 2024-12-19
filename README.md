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

