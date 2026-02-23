---
title: Solving problems
nav: RCA
topics: Root cause analysis; Critical thinking
---

## Before we solve a problem, wouldn't it be useful to know what's wrong?

<br>

### Let's talk burnout.

<br>



{% include jumbotron.html heading="Burnout " text="Exhaustion of physical or emotional strength or motivation usually as a result of prolonged stress or frustration." border=true %}

<br>

<br>

## Phsyician burnout

{% capture text %}

During the mid 2010s, roughly 50% of physicians were reported as experiencing professional burnout. This came at the same time that the healthcare industry was experiencing mass consolidation of corporate ownership and a flood of reimbursement issues with challenges to medicare/medicade/ACA and narrowing insurance networks. 

Organizational staff at the Mayo Clinic identified these trends to be unsustainable and developed a 9 step plan to address physician burnout.

{% endcapture %}
{% include card.html text=text img="Mayo_Clinic.jpg"%}


<br>

<div class="container">
  <div class="row">


    {% include modal.html button="Step 1" color="step-1" title="Acknowledge and Assess the Problem" text="Organizations must first recognize that physician burnout is a systemic issue and demonstrate that they care about their staff’s well-being. This involves regular, standardized assessment of burnout and engagement using validated metrics, which are then benchmarked against national data." %}

    {% include modal.html button="Step 2" color="step-2" title="Harness the Power of Leadership" text="The behavior of physician supervisors is a critical driver of burnout or satisfaction in their subordinates. Effective leaders must be identified, developed, and regularly assessed by the individuals they lead. Leadership training should focus on the ability to listen, engage, and develop physicians." %}

    {% include modal.html button="Step 3" color="step-3" title="Develop and Implement Targeted Interventions" text="Burnout drivers vary significantly by work unit and specialty. This strategy involves identifying 'high-opportunity work units' (those with the highest burnout rates) and implementing specific, local interventions based on the unique challenges of those units, such as streamlining clerical burdens or improving team communication." %}

    {% include modal.html button="Step 4" color="step-4" title="Cultivate Community at Work" text="Peer support is essential for physicians to navigate the challenges of medicine. Organizations should create dedicated spaces (such as physician lounges) and structured programs (such as small group meetings or shared meals) to foster interpersonal connections and reduce isolation." %}

    {% include modal.html button="Step 5" color="step-5" title="Use Rewards and Incentives Wisely" text="While productivity-based compensation is common, it can increase the risk of burnout if it incentivizes overwork or erodes quality of care. Organizations should consider incorporating quality and satisfaction metrics into compensation and using non-financial rewards, such as greater flexibility or protected time for meaningful work." %}

    {% include modal.html button="Step 6" color="step-6" title="Align Values and Strengthen Culture" text="An organization’s culture and its adherence to an altruistic mission (such as 'the needs of the patient come first') are vital for physician engagement. Leaders must ensure that organizational policies and day-to-day actions align with these shared values." %}

    {% include modal.html button="Step 7" color="step-7" title="Promote Flexibility and Work-Life Integration" text="Dissatisfaction with work-life integration is high among physicians. Organizations should offer options for adjusting professional work effort, such as part-time work or flexible scheduling, and comprehensively review vacation and leave policies to better accommodate personal responsibilities." %}

    {% include modal.html button="Step 8" color="step-8" title="Provide Resources to Promote Resilience and Self-Care" text="While not the primary focus, organizations should still provide individual tools for self-calibration and skills training in mindfulness, resilience, and positive psychology. These offerings are most effective when framed as part of a broader strategy that also addresses systemic issues." %}

    {% include modal.html button="Step 9" color="step-9" title="Facilitate and Fund Organizational Science" text="Leading organizations should invest in research to develop and test new evidence-based strategies for reducing burnout. This includes creating specialized programs or offices dedicated to physician wellness and generating new knowledge to improve the health care delivery system." %}

  </div>
</div>

<br>

>What the Mayo Clinic team had done was create an efficient machine to crowd source a root cause analysis.

<br>

{% include jumbotron.html heading="Root cause" text="The underlying reason why something happens or does not happen" border=true %}

<br>

The Mayo Clinic team focused on getting workers to voice their concerns and complaints regularly via one-on-ones, town halls, and open forums. This reduced the burden of discovery to only a few high-level administrators taking time out of their schedule to field these grievances and record them. 

<br>

>Throughout their investigation in developing the 9 step strategy the Mayo Clinic identified several systemic and local root causes contributing to physician burnout.

<br>

{% include accordion.html title1="Systemic Root Causes" text1="The problem is widespread and presents a pattern. These are often tied to organization level failure, executive administration, or policy." title2="Local Root Causes" text2="The problem is not widespread and does not present a pattern. These arise at an individual level and can be found in workers, middle management, and low level directors." %}

<br>

They identified 5 root causes for physician burnout across their locations:

1. Excessive EHR/documentation

2. Poor control over schedules

3. Lack of meaning in administrative tasks

4. Limited physician voice

5. Absent/apathetic leadership

<br>

{% include question.html header="Learning check" text="Which of the 5 root causes could be labeled as systemic?" solution="1, 2, 3, and 4." %}

<br>

<br>

---

## Worker burnout

{% capture text %}

Post-COVID, tech firms were noticing a problem of severe worker burnout. Despite the increase in commuting convenience that remote work culture had provided, worker turnover was rising while efficiency was plummeting. 

Research teams at Microsoft sought an answer for how to efficiently reverse this trend and began investing in organization level research into the root cause of tech worker burnout. 

{% endcapture %}
{% include card.html text=text img="microsoft.jpg"%}

<br>

### The Five-why Analysis

> The Five-why analysis is a powerful tool for root cause identification. Starting from the immediately observed problem, ask why that problem occurs until the fifth why or no more answers are possible. 

<br>

{% capture text %}

1. Begin with a problem statement.

2. Ask "why?" until you find the answer.

3. Identify the root-cause category.

{% endcapture %}
{% include card.html text=text header="Three steps to the Five-why analysis" %}

<br>

<br>

---

### **Problem statement**: Post-COVID, my remote workers are far less efficient.

<br>

## **Why?**

<br>

{% include modal.html button="Why? (1)" color="step-1" title="Lack of focus." text="Metrics show they're dedicating less time to their primary work tasks." %}

{% include modal.html button="Why? (2)" color="step-2" title="Less scheduled time." text="My workers have less scheduled time for their primary tasks than Pre-pandemic." %}

{% include modal.html button="Why? (3)" color="step-3" title="Increased scheduled meetings and collaboration." text="Every worker has had a significant increase in mandatory meetings and collaborative blocks like team office hours since we prioritized remote work." %}

{% include modal.html button="Why? (4)" color="step-4" title="We have to check in on them." text="We implemented increased meetings to make up for less in-office time so that we can keep track of the work our employees are doing and ensure they aren't wasting their time." %}

{% include modal.html button="Why? (5)" color="step-5" title="Leadership mistrust and overreach." text="The culture among leadership shifts more towards micromanagement and restriction than delegation and worker independence." %}

<br>

<br>

### **Categorize!**

<div class="container my-5">
  <div class="row row-cols-1 row-cols-md-3 g-4">

    <div class="col">
      <div class="card h-100 text-center shadow-lg border-3 border-primary">
        <div class="card-body">
          <h4 class="card-title fw-bold">Knowledge</h4>
          <p class="card-text">'We didn't know we needed to change.'</p>
        </div>
      </div>
    </div>

    <div class="col">
      <div class="card h-100 text-center shadow-lg border-3 border-primary">
        <div class="card-body">
          <h4 class="card-title fw-bold">Capability</h4>
          <p class="card-text">'We can't change.'</p>
        </div>
      </div>
    </div>

    <div class="col">
      <div class="card h-100 text-center shadow-lg border-3 border-primary">
        <div class="card-body">
          <h4 class="card-title fw-bold">Refusal</h4>
          <p class="card-text">'We don't want to change.'</p>
        </div>
      </div>
    </div>


    <div class="col"><div class="card h-100 text-center"><div class="card-body"><h5>Never knew</h5></div></div></div>
    <div class="col"><div class="card h-100 text-center"><div class="card-body"><h5>Missing resources</h5></div></div></div>
    <div class="col"><div class="card h-100 text-center"><div class="card-body"><h5>No reward</h5></div></div></div>
    <div class="col"><div class="card h-100 text-center"><div class="card-body"><h5>Forgot</h5></div></div></div>
    <div class="col"><div class="card h-100 text-center"><div class="card-body"><h5>Insufficient training</h5></div></div></div>
    <div class="col"><div class="card h-100 text-center"><div class="card-body"><h5>No penalty</h5></div></div></div>
    <div class="col"><div class="card h-100 text-center"><div class="card-body"><h5>Implied</h5></div></div></div>
    <div class="col"><div class="card h-100 text-center"><div class="card-body"><h5>Impossible</h5></div></div></div>
    <div class="col"><div class="card h-100 text-center"><div class="card-body"><h5>Disagreement</h5></div></div></div>

  </div>
</div>

<br>

{% include question.html header="Learning check" text="Which category of root cause does leadership mistrust fall into?" solution="Refusal." %}

<br>

Researchers at Microsoft collaborated with the University of Illinois at Urbana-Champaign (UIUC) to conduct a multi-faceted diagnostic effort on the problem of tech worker burn out. They paired systematic literature reviews with surveys, interviews, and cohort studies of tech workers to seek out the "infected node" in the work ecosystem. 

In the end they identified three root causes of worker burnout:

1. Synchronous meeting overload

2. Constant task switching

3. Always-on communication

<br>

{% include alert.html text="On your own or with your team, test the 5 why's for worker burnout. Do you agree that the three root causes identified by UIUC and Microsoft contribute to worker burnout?" align="center" color="success" %}

<br>

<br>

---

## Graduate Worker Burnout

{% capture text %}

On November 12, 2022 roughly 48,000 University of California system graduate workers went on strike for better pay, benefits, and protections. The strike ended on December 23, 2022 when the graduate worker union and university reached an agreement for roughly 70% pay increase, improved child care reimbursements, better health insurance for dependents/spouses, and supplemental tuition for international students. 

It's clear what the goal of the strike was, but why did it happen?

{% endcapture %}
{% include card.html text=text img="uc-strike.jpg"%}

<br>

In the months leading up to the UC graduate worker strike, UC administrators conducted internal investigations into what would relieve tensions. Their RCA was approach as a **structural assessment** and focused primarily on low level systemic and local root causes.

<br>

**When performing a root cause analysis there are two general approaches for asssessing the problem**:

{% include jumbotron.html heading="Structural assessment" text="Assessing the problem from an individual unit perspective (i.e., teams and departments)" border=true %}

<br>

Structural assessments are good for identifying local root causes and are less prone to missing issues hidden away at the lowest levels of organization.

<br>

{% include jumbotron.html heading="Systems assessment" text="Assessing the problem by observing how all the involved entities interact and produce results (i.e., workflows and organizations)." border=true %}

<br>

Systems assessments are better for isolating systemic root causes and observing the "bigger picture". They're prone to missing nuances at the individual level but less likely to bias towards placing blame on one entity.

<br>

{% include alert.html text="On your own or with your team, try to develop some potential root causes for the source of the UC graduate worker *strike*. Try to think past their demands and consider what could have caused a strike rather than union demands or lawsuits." align="center" color="success" %}

<br>

UC admins identified the following root causes for why graduate workers were burning out:

1. Over-working of graduate workers.

2. Food insecurity for graduate workers and faculty.

3. Systemic financial problems with the UC system.

<br>

> Failure to conduct a proper RCA can be catastrophic because it leads decision makers to place false confidence in the root cause.

<br>

The UC system decided to invest in growing their food bank networks for food insecure workers and capping student worker hours to prevent abuse of their "trainee" positions. Confident in their success, admins then refused to further negotiate with graduate workers. They later decided to increase worker wages by 4% with a promise to maintain that pace yearly.

<br>

The 4 week long strike was received with immense support from faculty and organizations such as the Teamsters. The strike resulted in university resources being witheld by delivery workers, final exams/grades being disrupted and canceled, and ceassation of all UC research activites for the duration of the strike. Every UC school had to implement special policies to make-up for undergraduate courses being disrupted to the point of degree program delays. 

The increase in pay that graduate workers originally argued for was still at the poverty line for the lowest cost of living parts of California. 

<br>

<br>

{% capture text %}

For want of a nail the shoe is lost, 

for want of a shoe the horse is lost, 

for want of a horse the rider is lost.

{% endcapture %}
{% include card.html text=text header="For want of a nail (George Herbert c. 1640)" %}

