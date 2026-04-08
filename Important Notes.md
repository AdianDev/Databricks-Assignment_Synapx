There are few points where I could have done better but as my current organisation project deadline is coming soon and we having back 2 back client calls. I don't have much time on my hand to take care of everything.

So, here are the improvements I was planning to make before improvement: 
1. In bronze table include an addtional metadata called version id which will track which has been already loaded to silver which one needs to be picked next in order to avoid repeating as we are loading 3 days of data. Therefore, the 3 times it will load for the same load_date if we follow the current logic.
2. In silver table I want CDF to be enabled. So, we can track the changes and can be applied to bronze as well than we might not need version id.
3. In gold layer introduce CDC based on silver table. So, if I a record is become inactive in silver it will get deleted from gold and only new or updated ones will be updated in silver.

So, these are the additional improvements I was thinking but I intentionally focused on delivering a clean, working Medallion architecture first.
Once that baseline was stable, I identified improvements like CDF-based change tracking and CDC-driven Gold layer to make it production-ready. 
