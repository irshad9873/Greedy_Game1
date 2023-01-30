# Greedy_Game1
SELECT us.user_id,us.app_id,
sum(last_login_date-signed_up_on)/count(distinct us.user_id)*APF*APV
	as user_LTV
from (
SELECT user_id,sum(total_revenue_in_paise)/count(offer_id) as APV,
count(rd.offer_id)/count(rd.reward_id) as APF
from user_offer_comp as uo
join reward_details as rd on uo.reward_id = rd.reward_id
group by user_id ) as new1
join user_signup as us
on us.user_id=new1.user_id
group by us.app_id,new1.apf,new1.apv,us.user_id
