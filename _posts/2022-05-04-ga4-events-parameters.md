# See Event Parameters in Google Analytics 4 Reports

## I. Reports

### Reports Realtime

You can see your event parameters in the real-time reports. In the image below, you can see the event parameters for the "Click" event, that track outbound links.

![Reports Realtime](https://boxxv.github.io/img/ga/event-realtime.png "Reports Realtime")

### Engagement Report

This event will also show up in the "Events" report as well as in the Engagement Report

The event report will show all the events on your site or app.

![Engagement Report](https://boxxv.github.io/img/ga/events-report-1024x241.png "Engagement Report")

Clicking on the event name will take you to the Engagement report, which will show you the events.

![Engagement Report](https://boxxv.github.io/img/ga/engagement-1024x494.png "Engagement Report")

## II. Custom Report

### Register Event Parameters as Custom Dimensions

Since there is a limit on the number of Custom Dimensions you can use, you have to thoroughly think through what parameter you want to register before going through the following steps

1. Click on "Custom Definitions" in the left navigation bar (Admin > Property column > Custom definitions )
2. Click on the "Create Custom Dimensions" button
3. Give you Custom Dimension a name. This is the name that will show up in your reports.
4. Select Event as the scope of the dimension
5. Provide Description (optional)
6. Select the event parameter that you want to use. If the event parameter does not exist yet then you can type the name that you will use. Keep in mind that this is case sensitive
7. Click Save".
8. Do 1 through 7 for every event parameter that you want to use in your reports

The event parameters can take up to 24 hours to show up in the reports so you might have to wait before you proceed with creating reports.

![Custom Dimensions](https://boxxv.github.io/img/ga/custom-definitions.png "Custom Dimensions")

### Using Event Parameters in Reports

1. Click on "Analysis Hub" in the left navigation bar ( Analysis --> Analysis Hub)
2. Click to create a new report create report using the "Exploration" technique.
3. Click on + sign next to Dimension to add new dimensions
4. Make sure to check the box next to "Event Name" and the event parameters that you want to use. This will make them available in the dimension section.
5. Drag and drop appropriate dimensions e.g. Event Name and Paramaters in this example on your report.
6. Add desired metrics

![Event Parameters](https://boxxv.github.io/img/ga/exploration.png "Event Parameters")
