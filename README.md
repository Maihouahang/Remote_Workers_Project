# Remote_Workers_Project: An Exploration of Trends in Remote Workers in the US

The Task
For this project, we are analyzing data from the Census Bureau to answer these following questions:

What are the most popular remote job fields?
What states do most remote workers live in?
How does the percentage of remote workers relate to the median household income across different states in 2022?
Have the numbers of female and male workers working from home changed over time?
How to Use
To determine the most popular remote job fields, begin by running the SIPP compiler file. This file makes the API calls to the Survey of Income and Program Participation 2022 database. In order to make these API calls, you will need a US Census API key, which can be easily acquired from the US Census website here. You will have to install the Census library by opening a jupyter notebook and typing "!pip install census"

You will either need to create a file in the main directory called 
c
o
n
f
i
g
.
p
y
.
Inside of your new config.py file, you will need to put the following code, replacing the text in the quotes with your API key:
api_key = "YOUR KEY HERE"
To ensure every aspect was considered, over 120 API calls were made, so it may take a while for all of them to run.
Running this will export a CSV file called full_worker_set into the Resources folder.
This contains all of the data necessary for running the statistics, but with a significantly reduced file-read time.
Now, we can quickly pull our API data from the generated CSV file by running the SIPP main file
This will also generate an intermediary CSV with income data for future statistical analysis.
At the bottom of the file, you will find pie charts looking at worker class, occupation type, and industry type for home-based workers. The summary pie charts are as follows:
Percentages of Home-based Worker Classes A pie chart showing percentages of home-based worker classes. Percentages of Home-based Workers' Top Occupation Types A pie chart showing percentages of home-based workers' occupation types. Percentages of Home-based Workers' Top Industry Types A pie chart showing percentages of home-based workers' industry types.

To answer question number 2 -

Run the Census_ACS_Data.ipynb file from step 1 to 7 to see how we analyzed the data. Run the Census_ACS_Data.ipynb file from step 8 to 10 to see how we created bar graph.

To answer question number 4 -

Run the Census_ACS_Data.ipynb file from step 11 to 13 to see how we analyzed the data. Run the Census_ACS_Data.ipynb file from step 14 to 17 to see how to see how we did a line regression.

Conclusions
To read the full report of our conclusions, please refer to our Remote Workers Analysis And Conclusion Report.

References and Acknowledgments
References from Mai's Branch

U.S. Census Bureau. (2021). American Community Survey 5-Year Data (2017-2021). U.S. Census Bureau. This website was used to hep us find the variables for workers who work from home and gender. Retrieved November 2024, from https://www.census.gov/data/developers/data-sets/acs-5year.2021.html#list-tab-1806015614

OpenAI. (2023). ChatGPT (Mar 14 version) [Large language model]. Accessed on Nov 2024. I, Mai Houa Hang, used this website for help with step 4 on the Census_ACS_Data.ipynb to get the data for all states. It helped me with providing me this code: geo={"for": "state:*"} to use. It also helped me with how to convert the list of lists to a DataFrame with this code: “wfh_df = pd.DataFrame(data[1:], columns=data[0])”. I learned to use the map function names_state dictionary and replaces the FIPS code with the corresponding state name. I also learned to use pd.concat to help me combine multiple DataFrames vertically (i.e., stacking them on top of each other). I also used the parameter “ignore_index=True” to help ignoring the existing row/index labels and generate a new index instead. I also learned from this website to use astype(int) to convert the values in my columns to intergers so I can calculate them to percentages. The website also helped provide this method to me: .apply(lambda x: "{:.2f}%".format(x)) so that I can format the percentage columns to two decimal places and put a % symbol in there. Retrieved from https://chat.openai.com/chat

OpenAI. (2023). ChatGPT (Mar 14 version) [Large language model]. Accessed on Nov 2024. I, Mai Houa Hang, used this website for help with step 5 on the Census_ACS_Data.ipynb to change the percentage column to numeric values and remove any % and commas. It helped provide this function for me to do those changes: "apply(lambda x: float(x.replace('%', '').replace(',', '')) if isinstance(x, str) else x". I learned to use the pivot method in this part of the code: "wfh_percentage_df = mean_df.pivot(index='State', columns='Year', values='Percentage of Workers Who Work From Home')" which helped me reshape the data. It transformed the data from a state-year combination to a separate state and separate year column. I also learned to rename the columns with this function: "#wfh_percentage_df.columns = [f"Percentage of Workers Who Work From Home ({year})" for year in wfh_percentage_df.columns]". This function helped me to label the columns to be the "Percentage of Workers Who Work From Home" for different years. It also provided this function for me: ".map(lambda x: f"{x:.2f}%" if isinstance(x, (float, int)) else x)". This function taught me to use the lambda function to every element in wfh_percentage_df. If the element is a number (either a float or int), it will be formatted as a percentage with two decimal places. Retrieved from https://chat.openai.com/chat

OpenAI. (2023). ChatGPT (Mar 14 version) [Large language model]. Accessed on Nov 2024. I, Mai Houa Hang, used this website for help with step 6 on the Census_ACS_Data.ipynb. It helped me to identify only the columns that contain the percentages (for each year) by providing me this function: "percentage_columns = [col for col in wfh_percentage_df_numeric.columns if 'Percentage of Workers Who Work From Home' in col]". It also helped me sort the DataFrame by those percentage columns by providing me this function: "wfh_percentage_df_sorted = wfh_percentage_df_numeric.sort_values(by=percentage_columns, ascending=False)". Retrieved from https://chat.openai.com/chat

OpenAI. (2023). ChatGPT (Mar 14 version) [Large language model]. Accessed on Nov 2024. I, Mai Houa Hang, used this website for help with step 8 on the Census_ACS_Data.ipynb. It provided me this function: "wfh_percentage_df_2020 = wfh_df[wfh_df['Year'] == 2020].set_index('State')" which helped me create a new DataFrame wfh_percentage_df_2020 that contains only the rows from the original DataFrame wfh_df where the 'Year' is 2020, with 'State' now serving as the index. It also provided me this function: "ax = wfh_percentage_df_2020['Percentage of Workers Who Work From Home'].plot(kind='bar', figsize=(14, 8))" which helped me to create a bar chart and specify the size of the bar chart. Retrieved from https://chat.openai.com/chat

OpenAI. (2023). ChatGPT (Mar 14 version) [Large language model]. Accessed on Nov 2024. I, Mai Houa Hang, used this website for help with step 12 on the Census_ACS_Data.ipynb with processing the data into a structured format. I used the .get(...'Unknown') and .get(...'None') method to help me with getting the values from the variables and returns either Unknown if they cannot locate the value or None if they cannot locate the value. Retrieved from https://chat.openai.com/chat

OpenAI. (2023). ChatGPT (Mar 14 version) [Large language model]. Accessed on Nov 2024. I, Mai Houa Hang, used this website for help with step 13 on the Census_ACS_Data.ipynb. I used this code from it: "to_numeric(....errors = 'coerce')". This helped me convert my column into numeric values and replace values that cannot be converted to a number to NaN. I used the pivot_table method to group and summarize the data, and the aggfunc parameter to find the average value for the 'Percentage Worked From Home' column for each state, year, and gender combination.I used this if statement from the website: "if pd.notnull(x) else None" checks whether the value x is NaN or None. If the value is not null, the function will format it as a percentage. If the value is null, it returns None instead of trying to format the value, which prevents errors when trying to apply the formatting to missing data. I used this code: gender_percentage_df.columns = [f"{year} {gender} Percentage Worked From Home" for year, gender in gender_percentage_df.columns] to help me make each column name is a single string that contains both the year and the gender to read the data easier. Retrieved from https://chat.openai.com/chat

OpenAI. (2023). ChatGPT (Mar 14 version) [Large language model]. Accessed on Nov 2024. I, Mai Houa Hang, used this website for help with step 14 on the Census_ACS_Data.ipynb. It helped provide this code to me: "female_data = female_data.dropna()" so that I was able to drop the rows with NaN values. Retrieved from https://chat.openai.com/chat

OpenAI. (2023). ChatGPT (Mar 14 version) [Large language model]. Accessed on Nov 2024. I, Mai Houa Hang, used this website for help with step 15 on the Census_ACS_Data.ipynb. It helped me with the if statement to make sure I'm able to collect the datas for the x and y value. It provided me the following codes: "if len(female_data) > 0: x = np.array([2020, 2021, 2022]) y = female_data.values.flatten() x_extended = np.tile(x, len(female_data))". Using len helped me checks if there is any valid data left after removing rows with missing values. Np.array helped with createing an array x to contain the years. y = female_data.values.flatten() helps to flatten the DataFrame into a 1D array y that contains all the percentages of female workers working from home for each state and year. If I don't use .flatten() it will not give me all the perecentages of female workers working from home. np.tile(x, len(female_data)) helped to create a new array where the years are repeated for each state in DataFrame. I was unable to create the scatter plot and had the website helped provide me with this code: "plt.figure(figsize=(8, 6)) plt.scatter(x_extended, y, color='red', label='Female data') plt.plot(x_extended, regress_values, 'g-', label='Regression Line') plt.annotate(line_eq, (0.05, 0.95), xycoords='axes fraction', fontsize=12, color="green")". It helped me figure out what figure size to use for my plot and it helped me with knowing to put x_extended there in after using the scatter method and plot method. It also heped me with the annotation. The annotate function place the regression equation (from line_eq) on the plot at the coordinates (0.05, 0.95) and it is displayed in green and with a font size of 12. Retrieved from https://chat.openai.com/chat

OpenAI. (2023). ChatGPT (Mar 14 version) [Large language model]. Accessed on Nov 2024. I, Mai Houa Hang, used this website for help with step 17 on the Census_ACS_Data.ipynb. It helped provide the function: "years = [2020, 2021, 2022]" for to use after the if statement and bfeore putting the x value. For some reason, it didn't pull from all three years so I had to include year in there for the data to pull. Retrieved from https://chat.openai.com/chat 

OpenAI. ChatGPT. Version 4, OpenAI, 2024, https://openai.com/chatgpt. Accessed 17 Nov. 2024. I Mee Thao Used ChatGPT to help code create loop in order to grab work-at-home and median household income. ChatGPT also helped converted the data frame to numeric for easy to read format. 

OpenAI. ChatGPT. Version 4, OpenAI, 2024, https://openai.com/chatgpt. Accessed 19 Nov. 2024. I Mee Thao Used ChatGPT to help plot a scatter chart as I was having issues with the bar chart. The code used plt.annotate to add the state names to the scatter plot which I thought was helpful.

I Mee Thao collaborated with Mai Houa Hang and Jacob Sickerman on 11/11/2024, 11/18/2024, and 11/19/2024.

I Susan Thao Vang collaborated with Mai Houa Hang and Jacob Sickerman 11/2024. Sources Used : SharkCoder. "Matplotlib Pie Charts." SharkCoder, 2021, www.sharkcoder.com/data-visualization/mpl-pie-charts. Accessed Nov. 2024. Geoapify. Geoapify, www.geoapify.com. Accessed Nov. 2024.
