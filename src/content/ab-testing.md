---
layout: post
title: How Can A/B Tests Go Wrong
image: img/feeling-proud.png
author: Pranay Aryal
date: 2019-08-16T10:00:00.000Z
tags:
  - Stats
---

#### Definition
A/B tests are popular these days but what are a/b tests.  A/b tests are done to see the effects of experiments on websites, campaigns or emails on outcomes such as sales or conversion.  You may want to serve one group of users one type of CTA button and another group of users with a different colored button.

  <button style="color: green; align:left;">Try For Free</button> <button style="color: red; align: right;">Try For Free</button>

You may change the text of the button for an experimental group of users and the existing unchanged button to another group of users.

<button style="color: green; align:left;">Try For Free</button> <button style="color: green; align: right;">Try For Free (no credit card required)</button>

#### Similarities  
They are similar to the biology experiments you did in school.  You want to test if covering a portion of a leaf (experimental leaf) will make it turn yellow (endpoint).  

But you use another leaf as a 'control'.  If this 'control' leaf does not turn yellow, you might conclude that it was the blocking of sun in the experimental leaf that caused it to turn yellow although you might have to repeat the experiment a few more times to get confidence.

'Controls' make the results of the experiments stronger than without them. However, there are pre-requisites for this which I will come to later.

Another analogy is the <strong>testing of new drugs for diseases.</strong>  Patients are randomly (this is important) to treatment/experimental group (who receive the drug),  and control group who receive the placebo or, commonly, the sugar pill.  

At the end of the experiment/trial, an endpoint such as survival is compared between the experimental and control groups. Now a lot of drug manufacturers, instead of using survival as an endpoint, use a different proxy or a surrogate such as progression of the size of cancer in CT scan, which they think is is the same as survival. But there can be problems with using surrogate outcomes like these, which is a topic for another blog.

A/b tests are similar.  A group of users is served the existing version (control) of the website and another is given a modified version (experimental)  At the end of the experiment, outcome such as conversion or sales is compared

As with all experiments, including those done by big drug companies and published in top journals, we need to look at them with a skeptical eye.  After all, a <strong>healthy skepticism</strong> is what has always kept science in check.

So to recap, a/b test, like drug trials,  have an experimental group, a control group and an endpoint that is measured in both groups.

What are some <strong>caveats</strong> to watch out for in a/b tests?

#### 1. If I repeat the experiment will I get the same result?
I can't stress enough how important this is in any science experiment.  This is known as <strong>reproducibility</strong>.  A good scientist always asks: did I get these results because of chance?  Will I get the same results if I repeat the experiment. 

#### 2. Am I measuring the correct outcome?

Conversion or sales are valid endpoints to measure as they matter the most to you.  It is like measuring survival if you were doing a drug trial or experiment.  Survival is a valid endpoint to use to compare between treatment and placebo groups because survival matters the most to patients.  

However, if the endpoint you are measuring in both groups, for example,  is to see how many users land on the checkout page, you may be incorrect.  This may be because of the simple fact that all users who visit the checkout page may not end up buying the product.


#### 3. Are my experimental and control groups similar in all aspects except the experiment being done?
This is such an important question too.  What if your experimental group were younger and had more females or teenagers? What if the experimental group had more weekends or holidays than the control group?  All these could skew the results and make you believe that your experiment is a success.  Be very skeptical.

#### 4. Do I have the correct sample size?
If you are coming to conclusions based on 10 or 15 or 20 users, then you are doing it wrong.  Just abandon a/b testing. Use your intuition.  If you are never going to get so many users, it is better to rely on your gut feeling.  Google and facebook and Quora can do experiments almost every day because they have a large user base.  For a website getting small traffic it is better to not waste time on a/b tests.

#### 5. Am I making one change at a time?
Make one change at a time and do the tests.  Making too many changes will muddy the results.  This point should be quite intuitive.  Let's say you are trying to see if weight training reduces the 6 week weight loss in treatment and control groups.  But a group of patients in the weight training group happened to also control their diet calories.  This is going to cause wrong results.

You are testing your call to action but the designer managed to slip in a few testimonials during production which was deployed along with the CTA changes.  This is going to cause problems.

#### 6. Can I just go with gut feeling?
It may be prudent to just go with gut feeling and not do a/b tests in these situations - your user base is low, you are not able to determine if the experimental and control groups are really similar in age, gender, time of experiment, your sample size is low.

#### 7. Don't trust advice given by people who run a/b testing companies.
This is known as financial conflicts of interest and is rampant in medicine.  It is in an a/b testing company's best interest to make you believe that you need a/b testing.  Don't fall for it.  In medicine, it is prudent to take the advice of speakers who are paid by drug companies, with a huge pinch of salt.  Drug companies try to game a drug experiment because it is in their best interest to make the drug look good in an experiment.

To summarize, be very skeptical of a/b tests.  If you are in doubt repeat the tests as many times as you can.  If you are in lots of doubt just abandon a/b tests and go with gut feeling.  A positive result could mean that your two groups are skewed.

I hope the above principles will help you be to have a skeptical outlook to anything in life.