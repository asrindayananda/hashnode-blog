## Create a budget alert in Azure cloud

Below are steps on how I set up a budget in Azure cloud so it alerts me before I spend too much. I hope this helps you as well.

- Sign in to your Azure portal
- Search for cost management and click on cost management. You will have a screen like below

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1643478083183/NeUmJctNe.png)

- Click on budgets on the right hand side
- Add a budget

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1643478095872/94eMcJrXU.png)

- Enter budget details 
- Set Budget name to whatever you like
- Set Reset period to monthly to reset the budget monthly as usually you are charged monthly unless you have changed do a different way to pay
- Set Creation date to the beginning of the month. This should be set for you
- Set Expiration date to whenever you want the budget to end, say 10 years time 
- Set your Budget amount, this is what amount you are willing pay
- My budget looks like this 

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1643478119003/dI0A-YOJm.png)

- Click Next after confirming
- Set Alert conditions 
- Select Type of actual or forecasted. Actual means amount of services used and charged for and forecasted means prediction of azure services depending on how you use them. Eg. if a virtual server is on most of the time it's going to predict how much it's going to spend. I prefer actual.
- Select % of budget, this percentage is when the percentage of budget you set in the   previous screen will send an alert to you. I like to set this at 90%. The Amount will be worked out for you automatically
- Action group is set to none
- Add Alert recipients emails to who you want alerts to go to
- Select language
- Click create

Congrats, You have created an alert
Now you will be notified when you are reaching your budget and there will be no nasty surprises.

More info at Microsoft docs https://docs.microsoft.com/en-us/azure/cost-management-billing/costs/tutorial-acm-create-budgets

# Shameless Plugs 
- [Join me and invest commission-free with Freetrade. Get started with a free share worth £3-£200.](https://magic.freetrade.io/join/asrin/447192e9)
- [Start a blog on Hashnode](https://hashnode.com/@azcodez/joinme)
- [Transfer money internationally with Wise](https://wise.com/invite/ath/asrind)

Feel free to comment if you get stuck or have questions or feedback✌️

Happy Coding 🙂
Az 👨🏾‍💻
