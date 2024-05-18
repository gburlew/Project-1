# Project-1
Observing trends regarding the Covid vaccines.

## Overview of the Project
Our main goal was to observe trends involving vaccination rates for the Covid vaccine. We plan to look at several open source datasets from around the world, specifically ones that focus on the rates of vaccination in different countries disaggregated by vaccine manufacturer, age groups and population sizes. This includes looking at differences between age groups and their preferences towards certain vaccines, vaccine rates in particular countries, and the total cases a country experienced.

### Research Questions
What countries had the highest/lowest vaccination rates?
What age groups appeared to have the highest vaccination rates?
Did the majority of the countries provided in this dataset have the same age groups that had the highest vaccination rates?
Were there any that deviated from the norm?
Manufacturer preference by age group?
  By country?
Did age group affect the total number of fully vaccinated, boosters or partial vaccinations?
Did some countries have less access to types of vaccines?
Covid cases vs vaccinations?

## Presentation
Below is the link to our presentation. This includes all of the graphs that we focused on, and the data that we found most beneficial to our research questions.
[Presentation Link]((https://docs.google.com/presentation/d/1WHaVupxndZSUvioeZD7LKLBjvfZAw6Gaf5VZwfP0sys/edit?usp=sharing))

## Navigating our Repository
Our repository has several resources and notebooks that we worked in. Below you can find links to the most important ones.
### Notebooks
The [main]((https://github.com/gburlew/Project-1/blob/main/Notebooks/main.ipynb)) notebook holds our merged drafts, and runs the code to get all of our graphs. We have several rough drafts that were used to merge into our main notebook, including the [analyzing total vax (rough)]((https://github.com/gburlew/Project-1/blob/main/Notebooks/analyzing%20total%20vax%20(rough).ipynb)), and the [covid cases vs vax]((https://github.com/gburlew/Project-1/blob/main/Notebooks/covid%20cases%20vs%20vax.ipynb)).

### Resources
The resource folder includes the csv files that we used to merge and analyze our data. Below are descriptions of the csv files.
- [full-data.csv]((https://github.com/gburlew/Project-1/blob/main/Resources/full_data.csv)): This file contains the total cases and deaths from covid for each country.
- [vaccinations-by-age-group.csv]((https://github.com/gburlew/Project-1/blob/main/Resources/vaccinations-by-age-group.csv)): This file disaggregates age groups based on the portion of the population that received a vaccine. The proportions are based on what percent of the population received a dose of the vaccine, including initial dose, second dose, and booster.
- [vaccinations-by-manufacturer.csv]((https://github.com/gburlew/Project-1/blob/main/Resources/vaccinations-by-manufacturer.csv)): Includes the number of doses of each brand of vaccine that were distributed per country. This is a count, not a proportion.
- [world-population-data.csv]((https://github.com/gburlew/Project-1/blob/main/Resources/world-population-data.csv)): This was the data used to calibrate for population. It included the 2022 populations for each country.

## Citing Sources:

Genevieve:
The code I paste here is code that xpert has helped me write. If the code comes from a different source, I will specify where it was from. Some code has since been edited in my project, but these are the foundations that I used.

import sys
sys.path.append('../')) from xpert

startdate = pd.Timestamp("2020-12-04")
enddate = pd.Timestamp("2024-04-17")

vaccinations_age_df['date'] = pd.to_datetime(vaccinations_age_df['date'])
vaccinations_manufacturer_df['date'] = pd.to_datetime(vaccinations_manufacturer_df['date'])
full_data_df['date'] = pd.to_datetime(full_data_df['date'])

vamask = (vaccinations_age_df['date'] >= enddate) & (vaccinations_age_df['date'] <= enddate)
vafiltered = vaccinations_age_df[vamask]

vmmask = (vaccinations_manufacturer_df['date'] >= enddate) & (vaccinations_manufacturer_df['date'] <= enddate)
vmfiltered = vaccinations_manufacturer_df[vmmask]

fdmask = (full_data_df['date'] >= enddate) & (full_data_df['date'] <= enddate)
fdfiltered = full_data_df[fdmask]

masks and timestamps, along with code to filter out dates that weren't in a certain range

age mapping dictionary

df['desired_age_group'] = df['age_group'].map(age_mapping)

got advice from my instructor regarding age groups that overlapped with the ones that i planned to present, and dropped the ones that would have overlapped through two or three different age groups. i decided to drop the age groups that had more than 1k instances of appearing in the dataset.

while i had an idea on what to do, i had trouble figuring out how to convey my data in a double bar chart to show the frequency of the most popular vaccine with the total count of each age group. i got the following code from xpert 
x= range(len(age_groups))
bar_width = .5
fig, ax = plt.subplots()
bar1 = ax.bar(x, group_count, bar_width, label='Vaccine Count', color='Green')
bar2 = ax.bar([i + bar_width for i in x], pfizer_count, bar_width, label='Group Population', color= 'Orange')

ax.set_xlabel('Age Group')
ax.set_ylabel('Vaccine Count')
ax.set_title('Pfizer/BioNTech Distribution by Age Group')
ax.set_xticks([i + bar_width / 2 for i in x])
ax.set_xticklabels(age_groups)
ax.legend()

********ax = testdf.pivot(index='new_age_group', columns='vaccine', values='total_vaccinations').plot(kind='bar')
ax.set_ylim(0, 10**11)

testdf = am_df[["total_vaccinations", "new_age_group", "vaccine"]].groupby(["new_age_group", "vaccine"]).sum()
testdf.reset_index(inplace=True)********* help from ali to create table showcasing most popular vaccines for each age group

vaccines_to_drop = ['CanSino', 'Covaxin']
df = df[~df['vaccine_type'].isin(vaccines_to_drop)]
from xpert

bar2 = ax.bar(x, group_count, bar_width, label='Group Population', color='Orange')

ax2 = ax.twinx()
line = ax.plot([i + bar_width / 2 for i in x], pfizer_count, color='Green', marker='o', label='Pfizer Count')
the code that was changed to create my graph with a secondary axis.

cmdfplot.reset_index(drop=True, inplace=True)
from xpert

more help from xpert regarding the locations to put some of my code, as i had some of it out of order.

cmdf_count_plot = cmdf_count.groupby("location")["unique"].count().reset_index() xpert had me add ".count()" before "reset_index()" in my original code because the groupby function wouldn't let me just do "reset_index"

cmdf_count = am_df.groupby("location")["vaccine"].unique().apply(len).reset_index(name='count')     i'd had trouble starting the code to create the next plot, as i kept using .groupby() on a dataframe that was already using the groupby function. xpert had me do this to get around this obstacle.

plt.xticks(rotation=90) i chose the angle of rotation, but xpert gave me the formula for it.

labels = ['CanSino', 'Moderna', 'Oxford/AstraZeneca', 'Pfizer/BioNTech', 'Sinopharm/Beijing', 'Sputnik V' ]
sizes = [0.41, 15.67, 18.33, 20.12, 29.46, 16.00]

selected_locations = ['Argentina', 'Austria', 'Hong Kong', 'Poland', 'Romania']

filtered_cmdfplot = cmdfplot[(cmdfplot['location'].isin(selected_locations))]
filtered_cmdfplot.reset_index(drop=True, inplace=True)

#Create the bar plot for the filtered data
ax = filtered_cmdfplot.pivot(index='location', columns='vaccine', values='total_vaccinations').plot(kind='bar')

#Set the plot properties
ax.set_ylim(0, 10**5)
ax.set_xlabel('Locations')
ax.set_ylabel('Vaccine Popularity')
ax.set_title('Vaccines Available in Different Countries')
ax.legend(loc="upper right")

#Show the plot
plt.show()
The above code comes from xpert helping me create the last graph that I ended up using for this project.
