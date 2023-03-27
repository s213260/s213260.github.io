---
layout: post
title:  "Analysis visualization"
date:   2023-03-27 15:32:52 +0200
categories: jekyll update
---
Here plots from the analysis will come
# Seting up the number of columns and rows for the grid of subplots
col_nums = 2
row_nums = int(len(focuscrimes) / col_nums)

# Figure size and title
fig = plt.figure(figsize=(17, 30))
fig.suptitle('Number of crimes per month by category from 2003 and 2018', fontsize=20)

# Define the x axes with the month names
months = ['January', 'February', 'March', 'April', 'May', 'June', 'July',
          'August', 'September', 'October', 'November', 'December']
#weekdays = ['Monday', 'Tuesday', 'Wednesday', 'Thursday', 'Friday', 'Saturday', 'Sunday']

# For Loop over each of the focus crimes and create a subplot for each one. Same than in the previous one.
i = 1
for crime in sorted(focuscrimes):
    # Creating a subplot for the current focus crime
    ax = plt.subplot(row_nums, col_nums, i)

    # Geting the counts of crimes for each month and create a bar plot
    counts = grouped_cat.get_group(crime).groupby("Month").count()['IncidntNum']
    plt.bar(months, counts, color='blue', alpha=0.6, linewidth=2) # edgecolor='navy'

    # Set the title, labels, and limits for the current subplot
    ax.title.set_text('')
    ax.set_ylabel('Crime count')
    plt.ylim(bottom=0)
    plt.xticks(rotation=90)

    # Add a legend for the current focus crime to the upper left corner of the subplot
    plt.legend(labels=[crime], loc='upper left', markerfirst=True, markerscale=0, frameon=False, shadow=False, handlelength=0)

    # Increment the counter for the subplots
    i += 1

# Adjust the spacing between the subplots and save the figure
fig.tight_layout()
fig.subplots_adjust(top=0.96)
