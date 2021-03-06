# Data Visualization and Data Refinery

Let's take a quick detour to the *Data Refinery* tool. Data Refinery can quickly filter and mutate data, create quick visualizations, and do other data cleansing tasks from an easy to use user interface.

This section is broken up into the following steps:

1. [Load the data](#1-load-data)
1. [Refine the data](#2-refine-data)
1. [Profile the data](#3-profile-data)
1. [Visualize the data](#4-visualize-data)

>*Note: The lab instructions below assume you have a project already and have data you will refine. If not, follow the instructions in the pre-work and import data to project sections to create a project and assign data to your project.*

## 1. Load Data

* Go the (☰) navigation menu and click on the *Projects* link and then click on your analytics project.

![(☰) Menu -> Projects](../.gitbook/assets/images/navigation/menu-projects.png)

* From the *Project* home, under the *Assets* tab, ensure the *Data assets* section is expanded or click on the arrow to toggle it and open up the list of data assets.

* Click the check box next to the merged data asset  *XXXAPPLICANTFINANCIALPERSONALLOAN* (where `XXX` is your username or the username of the person who granted you data access) to check it, then click the 3 vertical dots to the right, and select the *Refine* option from the menu.

![Launch the action menu](../.gitbook/assets/images/dr/dr-launch-table.png)

* Data Refinery will launch and open to the `Data` tab. It will also display the information panel with details of the data refinery flow and where the output of the flow will be placed. Go ahead and click the `X` to the right of the *Information* panel to close it.

![Data Refinery view](../.gitbook/assets/images/dr/dr-open-table.png)

## 2. Refine Data

We'll start out in the *Data* tab where we wrangle, shape and refine our data. As you refine your data, IBM Data Refinery keeps track of the steps in your data flow. You can modify them and even select a step to return to a particular moment in your data’s transformation.

### Create Transformation Flow

* With Data Refinery, we can transform our data by directly entering operations in R-style syntax or interactively by selecting operations from the menu. For example, start typing *filter* on the Command line and observe that autocomplete will give hints on the syntax and how to use the command.

![Command line filter](../.gitbook/assets/images/dr/dr-cli-filter.png)

* We will use the UI to explore and transform the data. Click the `+Operation` button.

![Choose Operation button](../.gitbook/assets/images/dr/dr-choose-operation-button.png)

* Let's use the `Filter` operation to check some values. Click on `Filter` in the left panel.

![Filter Operation](../.gitbook/assets/images/dr/dr-filter-operation.png)

* We want to make sure that there are no empty values in the *StreetAddress* column. Select the *`StreetAddress`* column from the *Column* drop down list, select *`Is empty`* from the *Operator* drop down list, and then click the `Apply` button.

![Filter is empty](../.gitbook/assets/images/dr/dr-filter-is-empty.png)

> *Note: If there are records where the selected column is empty, they will be displayed after clicking the apply button. If there are no records for this filter, it means that the 1000 rows we are previewing do not have any empty values for the selected column.*

* Now, click on the counter-clockwise "back" arrow to remove the filter. Alternately, we can also remove the filter by clicking the trash icon for the Filter step in the *Steps* panel on the right.

![Click back arrow](../.gitbook/assets/images/dr/dr-click-back-arrow.png)

* We can remove these records with empty values. Click the `+Operation` again and this time select the *Remove empty rows* operation. Select the *StreetAddress* column, then click the `Next` button and finally the `Apply` button.

![Remove empty rows](../.gitbook/assets/images/dr/dr-remove-empty-rows.png)

* Let's say we've decide that there are columns that we don't want to leave in our dataset ( maybe because they might not be usefule features in our Machine Learning model, or because we don't want to make those data attributes accessible to others, or any other reason). We'll remove the `FirstName`, `LastName`, `Email`, `StreetAddress`, `City`, `State`, `PostalCode` columns.

* For each columnn to be removed: Click the `+Operation` button, then select the `Remove` operation. Click the `Change column selection` option.

![Remove Column](../.gitbook/assets/images/dr/dr-remove-change-column.png)

* In the *Select column* drop down, choose one of the columns to remove (i.e `FirstName`). Click the `Next` button and then the `Apply` button. The columns will be removed. Repeat for each of the above columns.

* At this point, you have a data transformation flow with 8 steps. As we saw in the last section, we keep track of each of the steps and we can even undo (or redo) an action using the circular arrows. To see the steps in the data flow that you have performed, click the *Steps* button. The operations that you have performed on the data will be shown.

![Flow](../.gitbook/assets/images/dr/dr-final-flow.png)

* You can modify these steps in real time and save for future use.

### Schedule Jobs

Data Refinery allows you to run jobs at scheduled times, and save the output. In this way, you can regularly refine new data as it is updated.

* Click on the "jobs" icon and then `Save and create job` option from the menu.

![Click jobs icon](../.gitbook/assets/images/dr/dr-save-and-create-job.png)

* Give the job a name and optional description. Note that you can `Edit` the steps in this Data Refinery flow at this time. Also, note the output name, which in this case is *USER1006.JRTAPPLICANTFINANCIALPERSONALLOAN_shaped.csv*. Click the `Create and Run` button.

![Create and Run Refinery job](../.gitbook/assets/images/dr/dr-create-and-run-job.png)

* The job will be listed as *Status* *`Running`* and then the *Status* will change to *`Completed`*.

![Click Edit to schedule job](../.gitbook/assets/images/dr/dr-job-running.png)

* You can click `Edit` next to *Scheduled to run*. Notice that you can toggle the *Schedule to run* switch and choose a date and time to run this transformation as a job or even change the compute environment for this transformation. We will not run this as a job, go ahead and click the `Cancel` button

![Choose job scheduled time](../.gitbook/assets/images/dr/dr-job-settings.png)

### 3. Profile Data

* Go back to the top level of the data refinery view by clicking on the flow asset under the *'Associated Asset'* section in the scheduled job page.

![Back to refinery flow](../.gitbook/assets/images/dr/dr-flow-assset.png)

* Clicking on the *Profile* tab will bring up a view of several statistics and histograms for the attributes in your data.

![Data Refinery Profile tab](../.gitbook/assets/images/dr/dr-profile.png)

* You can get insight into the data from the views and statistics:

  * The median age of the applicants is 35, with the bulk under 49.

  * About as many people had credits_paid_to_date as prior_payments_delayed. Few had no_credits.

  * The median was 3 years for duration at current residence. Range was 1-6 years.

### 4. Visualize Data

Let's do some visual exploration of our data using charts and graphs. We can accomplish this in Data Refinery interactively without coding.

* Choose the *Visualizations* tab to bring up an option to choose which columns to visualize. Under *Columns to Visualize* choose *Age* and click the `Visualize data` button.

![Select Age column](../.gitbook/assets/images/dr/dr-vis-choose-column-age.png)

* We first see the data in a histogram by default. Looking at the distribution can give us insights. For example, there is a large bulk of applicants in the 18-20 year old range. Hover over that bar in the histogram and you can see that it is exactly 82 people in this sample data set.
The next histogram bar for 20-22 year olds is much smaller, with only 34 members in this cohort. These insights can help with finding gaps in our data, and aid in preventing bias and building a more accurate predictive model.

* You can edit the details of the chart in the left panel. In this case, you can choose to further refine this visualization by splitting the `Age` histogram by using the `Risk` column. So we will have a visualization of distribution of age for customers that churned and another for those that did not churn.

![Visualize Age column](../.gitbook/assets/images/dr/dr-vis-split-age.png)

* You can choose other chart types. Let's build a `Scatter plot` next. Click on `Scatter plot` as the 'Chart Type' in the top panel and then click the *`Continue`* button when prompted in the *Switch charts?* window.

![Switch to scatter](../.gitbook/assets/images/dr/dr-vis-switch-scatter.png)

* In the scatter plot, choose *Age* for the x-axis and *LoanAmount* for the y-axis. Choose *Age* for the Color map and *LoanAmount* for the Size map. Give it a title.

![Visualize Age and LoanAmount histogram](../.gitbook/assets/images/dr/dr-vis-scatter-plot.png)

* You can see an expected correlation between age and loan amount, with a nice graphic representation using color and size. Play around with the parameters, and feel free to choose other columns to visualize. You can also choose other Chart types.

* Under the `Actions` panel, notice that you can perform tasks such as *Start over*, *Download chart details*, *Download chart image*, or set *Global visualization preferences* (_Note: Hover over the icons to see the names_).

* Click on the "gear" icon in the `Actions` panel. We see that we can do things in the *Global visualization preferences* for *Titles*, *Tools*, *Theme*, and *Notifications*. Click on the `Theme` tab and update the color scheme to *Dark*. Then click the `Apply` button, now the colors for all of our charts will reflect this. Play around with various Themes and find one that you like.

![Visualize set theme and choose preferences](../.gitbook/assets/images/dr/dr-vis-choose-theme.png)

### Conclusion

We've seen a small sampling of the power of Data Refinery on IBM Cloud Pak for Data. We saw how we can transform data using R code, at the command line, or using various Operations on the columns such as changing the data type, removing empty rows, or deleting the column altogether. We next saw that all the steps in our Data Flow are recorded, so we can remove steps, repeat them, or edit an individual step. We were able to quickly profiile the data, so see histograms and statistics for each column. And finally we created more in-depth Visualizations, creating a scatter plot mapping TotalCharges vs. MonthlyCharges, with the Churn results highlighted in color.
