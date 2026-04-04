---
layout: post
title:  "Building Our Custom Wedding Website"
---

My partner and I recently got married! We feel incredibly grateful that everything went nearly perfectly, and we are really enjoying this new chapter in our lives together.

This post is about something that's usually a minor detail in most people’s wedding planning, but became a bit more of an adventure in ours -- the wedding website.

Like almost everything about our wedding day, we ended up having strong opinions about how our website should look and work. Although there are of course many platforms that tailor to this industry, I couldn’t pass up the opportunity to build our vision into reality from scratch. I ended up creating a fully custom wedding website with QR-code authentication, RSVP tracking, a purpose-built gift registry experience, and production-grade monitoring -- because I couldn’t help myself.

*Note: for our privacy I’ve replaced the photos, names, and details in the website screenshots throughout this post.*

## The Vision

At the end of the day, we had three specific requirements that I designed towards:

### Professional and Consistent Feel

Almost every aspect of a wedding can be obsessed over and tweaked to the couple’s satisfaction, but the website is frequently not among these details. I personally was willing to spend more time and money to have a website experience free of advertisements, unwanted links and logos, or unchangeable components that could detract from the guest’s experience.

<a class="float-left" href="/assets/img/wedding/registry.png" data-lightbox="registry">
    <img src="/assets/img/wedding/registry.png" alt="Screenshot of the wedding website's registry page, showing multiple purchasable items such as checked bags, taxi fares, dinner for two, and a night at a hotel." />
</a>

I find that this is especially true when dealing with an online Gift Registry, which often bounces guests through multiple other websites and can be confusing to navigate. A lot of wedding websites will also have a general Cash Fund option in their registry implementation, but our vision was to be more specific and allow our guests to choose exactly what experience they were contributing cash to, if they chose to do so. We felt that this created a much more satisfying and intimate gift giving experience, even if the end result is still just giving cash.

Obviously, building a website from scratch isn’t the *only* way to achieve this goal of consistency in design and experience, but for me having complete control over every minor aspect of the site was a benefit that I was glad came along with that choice.

### Privacy

Our wedding day and the surrounding details are uniquely personal. I find it quite jarring that many couples' wedding websites are left open to the world, with details of where and when the events are taking place, and maybe even an intimate writeup of the couple’s history together.

Protecting these details matters a lot to me. The simplest approach is password-protecting the site, but that introduces usability issues. For example, what if someone loses their invitation with the password? Or if using a password which is supposed to be common knowledge about the couple, how can you guarantee the recipient will know that piece of trivia to use to gain access to the website?

By contrast, we wanted our wedding details to be very secure and only accessible to those who had received an invite, not just anyone who knew a thing or two about us, and certainly not by everyone on the internet. At the same time, we wanted to avoid any technical challenges this would place on our guests. There are probably some wedding website platforms which have sufficiently solved this problem for their users, but if so, I haven’t personally seen it yet.

I wanted to achieve a simple but secure mechanism for accessing the website, that didn’t feel like a burden or afterthought to guests.

### Customized Invitations and Ease

<a class="float-left" href="/assets/img/wedding/rsvp-qr.png" data-lightbox="rsvp-qr">
    <img src="/assets/img/wedding/rsvp-qr.png" alt="Photo of an insert into the wedding invitation that says 'RSVP by August 15th' and contains a QR code to scan to access the wedding website." />
</a>

We decided to have each invitation come with a unique QR code that the recipient could use to quickly access the website and be authenticated ***as them*** in order to get more details about the wedding day and to RSVP.

The QR code embedded authentication info for the recipient of the invitation, and when scanned would instantly log them in to the site without any need for a password. However, when considering the breadth of background and age groups who would be receiving the invitation, I knew some people would be much more comfortable logging in to the website on a desktop computer rather than RSVP’ing from their phone.

<div class="clear" />

With this in mind I built a secondary authentication mechanism if someone didn’t come from a scanned QR code:

<a href="/assets/img/wedding/login.png" data-lightbox="login">
    <img src="/assets/img/wedding/login.png" alt="Home page of the website in an unauthenticated state, contains a photo of the couple and a login box that has a 'Last name' field and a 'House number on your invitation' field with an 'Enter' button underneath." />
</a>

Rather than relying on a password or “trivia check,” I wanted to allow invitees to access the website using something that would uniquely identify them, and something they (or at least those close to them) would know. I landed on a combination of using last name and house number, which makes it both easy to uniquely identify a household that had received an invitation, as well as *reasonably* difficult to guess someone's log in information. I used just the house number, instead of the full address, since addresses can be written in multiple ways that would be hard to programmatically match (for example `123 Main St` vs. `123 Main Street`).

Obviously, many of the households invited to the wedding knew each other well enough to know each other’s street addresses, and as such would be able to log in as one another in theory, so I was assuming some basic level of best intentions from those who had received an invite not to try and do this.

<a href="/assets/img/wedding/rsvp-cmd.png" data-lightbox="rsvp-cmd">
    <img class="tall-image" src="/assets/img/wedding/rsvp-cmd.png" alt="Photo of the same insert into the wedding invitation containing a QR code, however below the QR code is a monospaced textbox with pre-formatted curl commands that will RSVP the recipient and their plus-one to the wedding." />
</a>

On the other side of the coin, a lot of my groomsmen and some guests were also software engineers, so for the technically-minded guests I wanted to lean even more into the bespoke nature of this website and make them go directly to the website’s API to submit their RSVP.

Why? Because imagining my friends receiving a formal wedding invitation in the mail and having to open up a terminal and run curl commands to RSVP to it brought a smile to my face, and isn’t that what this is all about?

## Writing Software is my Love Language

I could write a long explanation justifying why our specific requirements (and my curl-RSVP gag) warranted building this website from scratch instead of using one of the many platforms available for building wedding-focused websites, but that would just be rationalization. The truth is that I did this because I really wanted to, and because I knew it would be a unique and fun challenge that would result in an experience that’s very authentic to who I am.

One of the things my partner and I both love as guests in attendance at a wedding is when an aspect of the couple’s ceremony is quintessentially *them*. It is so delightful and memorable to see a small touch that speaks directly to who they are and what they value.

Authenticity is something we both tried to keep in mind a lot through the process of planning our wedding, and for me, this is one of those authentic things -- being a software engineer is a big part of who I am and what I love to do. The reason I originally fell in love with programming, first as a hobby and then later as my career, is the satisfaction I get from crafting the perfect solution to a (sometimes incredibly niche) problem. Tinkering and building things using computers is a big part of my life, and I simply couldn’t say no to the delight and satisfaction this would bring me as part of our wedding planning process.

## How It’s Made

The frontend of the website is built using React. I evaluated a bunch of React UI libraries and landed on [Chakra UI](https://www.chakra-ui.com) because of the simple visual design, feature-richness and flexibility of its components. I am NOT a UI designer so I really needed all the help I could get to have a consistent and pleasing visual feel. I ended up being very pleased with Chakra and will definitely use it for more projects going forward.

Because the site is dynamic, it also needed a backend, which I built using TypeScript Lambda functions reading from and writing to DynamoDB. To cleanly communicate between the frontend and backend, I used [Zod](https://github.com/colinhacks/zod) to model all the request and response objects, which allowed me to quickly formulate, validate, and process requests and responses sent between the client (i.e. frontend) and server, for example:

```ts
export const RsvpRequestSchema = z.object({
    invitationId: z.string(),
    invitationRsvp: z.nativeEnum(RSVP),
    message: z.string().optional(),
    guestRsvps: z.array(GuestRsvpSchema),
}).strict();
export type RsvpRequest = z.infer<typeof RsvpRequestSchema>;

export const RsvpResponseSchema = z.object({
    error: z.string().optional(),
    message: z.string().optional(),
}).strict();
export type RsvpResponse = z.infer<typeof RsvpResponseSchema>;
```

I was also really happy with my choice in Zod, which I had never worked with before but picked because it’s TypeScript-first. At work, we use [Smithy](https://smithy.io) to model our APIs and generate client and server boilerplate code, but I felt that it was a bit overkill for this relatively simple project. Also, since the Smithy code generator is built in Java, I would need to pull in another build tool to use it. While I’m not always TypeScript’s biggest fan, I felt that being able to use one language across the entire project was a huge plus in simplifying things and accelerating development in this case.

The actual API was hosted on API Gateway, and both the API and the website were served using a CloudFront distribution which not only served the content quickly but also allowed me to easily add authentication logic to all of the access points. I used AWS’ [Cloud Development Kit (CDK)](https://docs.aws.amazon.com/cdk/v2/guide/home.html) to model and deploy all of this infrastructure.

Below is a diagram of the complete architecture:

<a href="/assets/img/wedding/architecture.drawio.png" data-lightbox="architecture">
    <img class="tall-image" src="/assets/img/wedding/architecture.drawio.png" alt="Architecture diagram of the wedding website built on top of AWS. Shows a user making requests to a CloudFront distribution, which returns website assets from S3 buckets, and sends API requests to API Gateway, backed by Lambda functions and DynamoDB. An event-bridge rule is also used to periodically invoke a canary lambda function to test the website." />
</a>

I was happy with all of these architectural choices, and the cost monthly was reasonable to me. Although a CDN does seem a bit extreme for this usecase, CloudFront cost me less than a dollar a month -- the main expense was (as per usual) CloudWatch. I wasn't willing to compromise on the number of metrics I had available to determine if something was going wrong, but damn do they really get you there. I'll talk more about my overkill monitoring in just a bit.

## The Result

### The usual stuff, and getting access to it

The website has all the standard pages you’d expect on any wedding website -- a homepage with a countdown timer, a bit about my wife and I’s story, some info about the people in our wedding, a page with locations, times, and details, and an FAQ. All of this stuff isn’t really interesting from a technical perspective, but I did spend a lot of time making it just what we wanted, so I’m still proud of it.

<div class="gallery">
  <div class="gallery-item">
    <a href="/assets/img/wedding/home.png" data-lightbox="gallery">
      <img src="/assets/img/wedding/home.png" alt="The homepage of the website once authenticated, shows a photo of the couple and a countdown timer to the wedding day." />
    </a>
    <div class="desc">Home page</div>
  </div>
  <div class="gallery-item">
    <a href="/assets/img/wedding/location.png" data-lightbox="gallery">
      <img src="/assets/img/wedding/location.cropped.png" alt="The 'Location' page of the website, shows information about the venue, the wedding day schedule, transportation and lodging options, and things to do while in town." />
    </a>
    <div class="desc">Location and day-of info</div>
  </div>
  <div class="gallery-item">
    <a href="/assets/img/wedding/story.png" data-lightbox="gallery">
      <img src="/assets/img/wedding/story.cropped.png" alt="The 'Our Story' page of the website, shows photos of the couple and lorem ipsum text in place of a narrative of how they met and got engaged." />
    </a>
    <div class="desc">Our Story</div>
  </div>
  <div class="gallery-item">
    <a href="/assets/img/wedding/party.png" data-lightbox="gallery">
      <img src="/assets/img/wedding/party.cropped.png" alt="The 'Wedding Party' page of the website, shows profile pictures of the maid of honor and bridesmaids, and the best man and groomsmen." />
    </a>
    <div class="desc">The Wedding Party</div>
  </div>
  <div class="gallery-item">
    <a href="/assets/img/wedding/faq.png" data-lightbox="gallery">
      <img src="/assets/img/wedding/faq.cropped.png" alt="The FAQ page of the website, shows questions and answers such as 'When is the RSVP deadline' and 'Can I bring a guest' along with lorem ipsum responses to each." />
    </a>
    <div class="desc">FAQ Page</div>
  </div>
</div>

As mentioned earlier, I wanted to tightly control access to all of this information. While a simple password would have sufficed, I was afraid that it would be easily lost, locking guests out of the website. Also, I wanted the ability to identify *who* was accessing the website for the more custom functionality discussed later, not just to verify that they should be authorized to access it. So I built my own authentication mechanism. In fact, I built two of them.

#### Authentication

I decided that I needed two mechanisms by which guests could access our website. One for guests who received our invitations to simply scan the included QR code and instantly be authenticated and granted access, and another in case guests wanted to log in on a device other than a mobile phone with access to a camera -- this latter one could also double as a backup mechanism in case they lost their invitation.

For each household receiving an invitation, I created an entry in our DynamoDB table. For example, an invitation could be represented as:

```json
{
 "InvitationId": "ABCD1234",
 "InvitationName": "Mr and Mrs John and Jane Smith",
 "Address": "123 Example Way Leesburg, VA 20176",
 "HouseNumber": "123",
 "LastNameLowercase": "smith",
 "LoginCount": 0,
 "RsvpChangeCount": 0,
 "Version": 0
}
```

For the easy QR code access mechanism, I encoded the unique `InvitationId` into the URL in the code, for example:

```
https://demo.wedding/rsvp?invitationId=ABCD1234
```

When the user scans the QR code, the request to `/rsvp` is intercepted by a [Lambda@Edge](https://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/lambda-at-the-edge.html) function. The interceptor queries DynamoDB for the provided `invitationId`, and if it is able to find it, logs the user in and stores a session cookie in their browser, allowing them access to the website. The result is a seamless experience where the user is uniquely authenticated and doesn’t even realize it’s happened.

![A zoomed-in image showing the login box seen earlier in the unauthenticated login page.](/assets/img/wedding/login-box.png){:.float-left}

For the manual login experience without a QR code, I built a page that users who attempt to access the website without having an `invitationId` in their URL parameters are forwarded to.

The login page asks for the guests’ last name along with their house number on the address their invitation was sent to. This information is sent to the backend API (also just a Lambda function), and if a matching invitation is found, the user is similarly logged in and has a session cookie stored in their browser.

<div class="clear"/>

Neither of these mechanisms are *extremely* secure and are fairly easily defeatable with a brute-force attack to try and guess the required information to log in. There’s likely exactly zero bad actors on the internet who care about accessing my wedding website, but I take putting things online very seriously, and never assume the best. Therefore, I took the additional step of implementing a throttling mechanism for the login systems that would defend against brute-force attacks. Since this was a generic tool I will definitely be re-using in future projects, I broke that library out and put it on GitHub here: [https://github.com/gravitylow/ddb-token-bucket](https://github.com/gravitylow/ddb-token-bucket).

If this throttling mechanism was ever engaged, I would be alerted and could use AWS tooling to manually block the traffic altogether. Thankfully, this never happened, but it was still good peace of mind for me having it just in case.

### The custom stuff

There are two pages on the website that made up about 90% of the complexity of this project -- those are the RSVP functionality and the gift registry. These inherently require a lot more going on under the hood to make them work compared to the other relatively static pages, and, especially in the case of RSVPing, are pretty essential to get right so they work 100% of the time. They also happen to be where we had strong feelings about how they should behave, and I spent lots of time experimenting, testing, and customizing them to be what we wanted and needed.

#### RSVP

From the beginning, this is what I knew I would most enjoy coding from scratch, because although it’s relatively simple functionality on its face, a number of things have to come together to make it happen well, and even more to iron out bugs and weird edge cases.

Since we opted to have a plated dinner at our reception, we needed to know more than just how many people were coming. We needed to have a list of who specifically was coming to place them on our seating chart, along with their meal choice and any dietary restrictions. This included any Plus Ones, so I’d need a way to allow guests to provide their names and meal information in the RSVP form too.

I also wanted to include a way for people to confirm whether or not they had already RSVP’d (I have been known to be guilty of not doing it promptly when receiving an invitation and then not remembering whether I had or had not already... I will no longer be guilty of that going forward having now gone through this experience myself) and a way for people to change their RSVP up to a certain date.

Here’s the representation of a Guest I ended up modeling in DynamoDB:

```json
{
 "GuestId": "WXYZ6789",
 "InvitationId": "ABCD1234",
 "GuestName": "John Smith",
 "RequiresName": false,
 "MealChoice": "CHICKEN",
 "RSVP": "YES",
 "RsvpChangeCount": 1,
 "Version": 1
}
```

The `RequiresName` field indicates to the frontend whether the user must provide a name for this guest when setting their RSVP to `YES`. The user can also opt not to bring a plus one and just set their RSVP to `NO` without providing a name or a meal choice.

Here’s how the final UI ended up looking in the RSVP interface:

<a href="/assets/img/wedding/rsvp.png" data-lightbox="rsvp">
    <img class="faded-image" src="/assets/img/wedding/rsvp.cropped.png" alt="The RSVP page of the website, showing RSVP options for one guest and their plus-one. Under each guest name there are options for whether or not they are attending as well as a dropdown to select their meal choice. There are also text boxes to enter any dietary restrictions or accommodation requests." />
</a>

The frontend performs validation to ensure all of the input is valid, and of course this validation is duplicated on the backend before accepting the RSVP change.

When a guest changed their RSVP, we eagerly wanted to know. So, I also integrated our backend with Simple Email Service (SES) to send my wife and I a simple email update whenever this happened:

<a href="/assets/img/wedding/rsvp-email.png" data-lightbox="rsvp-email">
    <img class="tall-image faded-image" src="/assets/img/wedding/rsvp-email.cropped.png" alt="A screenshot of Gmail on iOS. An email is open with the subject 'Thomas Becker RSVP'd YES for 2' and the email body contains information about the guest and their plus one's RSVP details, including their meal choice and dietary restrictions." />
</a>

#### Registry

Our wedding registry was the other big task to implement from scratch, because we had a fairly unique vision for it. Rather than going a more traditional route and having our guests buy us physical items, we wanted to allow them to contribute to specific experiences on our honeymoon. As I mentioned before, we felt that having a general “cash fund” might be both disappointing to a lot of people who would want to give something specific, and also give us less of an opportunity to be grateful for the specific thing they had contributed towards.

Our vision for the registry was therefore to have a set list of specific additions we could allow guests to contribute towards on our honeymoon.

<a href="/assets/img/wedding/registry.png" data-lightbox="registry">
    <img src="/assets/img/wedding/registry.png" alt="Screenshot of the wedding website's registry page, showing multiple purchasable items such as checked bags, taxi fares, dinner for two, and a night at a hotel." />
</a>

I had never integrated with any payment processor before, so I had a lot to research and learn here. I was aware that Stripe was by far the most popular payment processing API, but at the time I started on this project, Stripe's CEO had just posted a [tweet](https://x.com/patrickc/status/1861749249043796000) that was at best tone-deaf and at worst in tacit support of Israel’s ongoing genocide in Palestine. I strongly believe that software engineers have a responsibility to build ethically, so given that I wasn’t already locked in to anything, I decided it would be worth some additional time to find a platform that I felt comfortable using. I landed on Square, which has great [product and inventory-management functionality](https://squareup.com/help/us/en/article/7982-manage-square-online-item-settings-from-your-item-library) which I was excited about integrating with in order to allow my then-fiancée to easily help populate the list of honeymoon items without dealing with the code.

After getting all the code written for listing and displaying the inventory along with photos and descriptions, everything was working. The only thing I had to deal with myself was sending payment receipts, since I couldn’t find a way for Square to send them to the user themselves.

## Rehearsal

With all this done, and a bunch of tweaking and bugfixing, all of the core functionality of the website was done! I throw my laptop in my backpack and hopped on the train up to New York City to see my younger brother, who also happens to be both my most trusted software engineering counterpart and Best Man in our wedding, to put it to the real test.

<div class="center">
    <img class="nyc-pic" src="/assets/img/wedding/nyc-bugbash.jpg" alt="A photo of two beers on a desk with a code editor and chrome open in the background, with text that says 'It's bugbash time!'" />
    <img class="nyc-pic" src="/assets/img/wedding/nyc-carter.jpg" alt="A photo of my brother and I in Central Park" />
</div>
 <div class="clear" />

### Trouble in Squaradise

Sometime around 1:30am after hours of bashing website bugs, we ran into a problem we couldn’t figure out. Suddenly, the registry wasn’t working and was returning vague 403 errors in the console when we tried to complete a payment. I had been hot-fixing some bugs and deploying straight to the website so I tried to roll a few of these changes back with no success. My brother had a hunch that we had triggered some sort of fraud detection with our testing and prompted me to log in to Square, where sure enough I had a notice that my account required “additional information” in order to continue. I filled out the information they had requested from me, but in the morning I woke up to the following email:

<a href="/assets/img/wedding/square-deactivated.png" data-lightbox="square-deactivated">
    <img src="/assets/img/wedding/square-deactivated.png" alt="A screenshot from Gmail. The email's subject is 'Square Account deactivated' and the email body states that the square account has been deactivated as square is unable to support the business needs based on the information provided. It goes on to cover details about what happens next with the account balance." />
</a>

I feel like I *do* actually understand this response, to an extent -- I wasn’t operating a business, and this use case surely didn’t fall into any normal pattern Square would care to prioritize. I was still pretty disappointed by this turn, especially considering the swiftness of the action and the amount of work I had put in to integrate with Square over another platform. Most of all, I was **incredibly** thankful for all the time we spent testing this integration to trigger this issue before the website went live. I had done *extensive* testing myself prior to our bug-bashing weekend and was pretty sure we were good to go. I can’t imagine how much worse this would have been if guests had started to use Square to actually buy wedding gifts before they decided on an inquisition and account closure.

So, I went back to Google to find another payment processor, this time making sure that they would support my weird use case.   Despite how great it was to have the full Square interface for managing inventory without changing the code, I was pretty burnt out and unwilling to rewrite all 600+ lines of code I wrote to integrate completely with the Square platform and dynamically retrieve the items and inventory from their system (I also had a policy against using AI to write any for this project -- authenticity!). So, I opted for a much simpler approach where the inventory was hardcoded in the website client-side, and PayPal was used to process payments for the selected items.

```tsx
export const REGISTRY_ITEMS: RegistryItem[] = [
    {
        id: 'checked-bags',
        title: 'Checked Bags',
        cost: 50,
        available: 4,
        image: 'checked-bags.jpeg',
        description: "...",
    },
    // ...
]

return <SimpleGrid>
    { REGISTRY_ITEMS.map(item => (
        <RegistryItem key={item.id} item={item} />
    ))}
</SimpleGrid>
```

While this wouldn’t be a viable approach for purchasing real items, since it essentially would allow a technically savvy user to name their own price during check out, it was good enough for our use case where we were simply accepting gifts from website users. If anyone wanted to “cheat the system” and give a gift for less money than it “cost,” that would be fine by me.

So, we were back in business with PayPal and I sent the updated website off to my brother to pressure-test while I worked on an automated test suite.

### Integration Testing and Canaries

As overkill as it might be to have a canary running automated tests against your wedding website, I did have a deep fear that something would go wrong and nobody would be able to RSVP to our wedding due to some bug in my code. And, I felt this from-scratch challenge wouldn’t be truly complete until I implemented everything I would actually implement for a production system I would be comfortable delivering to a client, which definitely involves testing and monitoring in production. I wanted to be the first one to know if and when I broke something with a change, or something out of my control like the Square debacle happened again.

I put together a Lambda that used the [Playwright](https://playwright.dev) test framework to interact with the wedding website in production and exercise all of the functionality I cared deeply about working, especially RSVPing. Although playwright does support both UI testing as well as raw API tests, I opted to just write the UI tests since I didn’t care as much about direct usages of the API in this case. I figured that any usage that would be exercised through my testing of the website frontend would cover what users would care about.

<a href="/assets/img/wedding/canary-metrics.png" data-lightbox="canary">
    <img class="faded-image" src="/assets/img/wedding/canary-metrics.png" alt="A snippit of a CloudWatch Dashboard showing canary lambda metrics, including TPS, errors, latency, and throttling" />
</a>

This is the part where I could have used some lessons from my prior engineering experience a bit better. Every time I have written code that is meant to automate web browser usage running on Lambda, I feel as though I have directly accelerated the progress of my male-pattern balding. I may be naive in this area of software development, but there is absolutely **no** reason that this should be so difficult. Doing this months out from my wedding and pulling my hair out trying to get every one of the dependencies and Chrome command line arguments absolutely correct so that everything plays nicely together in a headless, serverless environment (where you can’t test the behavior until you deploy to that environment!!) seems like an exercise in pure insanity.

In order to get everything reliably working, I ended up writing a lot of boilerplate wrapper logic for the tests that would capture screenshots and logs of any of the test failures and upload them to an S3 bucket so I could understand what had occurred remotely.

Through an extremely long and arduous process of trial, error, and inventing new swear words, I was finally able to get the tests reliably working, and set up an EventBridge rule to run them every 10 minutes and publish metrics for their results. [Here's](https://gist.github.com/gravitylow/c404d461ade92e6cb061877c8a8c45af) the lambda function code I ended up with, which *mostly*, **usually**, works, although is not nearly as clean and locally-testable as I was envisioning when I started writing the playwright tests.

### Metrics and logs

In addition to the canary metrics and metrics emitted by the server, I also created an API endpoint for the website to post metrics and logs from the client’s perspective so that I could have a full view into the performance of the website, and be alerted of any issues I needed to know about. The website creates a singleton that collects metrics and logs posted from each component, and then peridocally flushes them in the background to the server with an API call:

```ts
import {Client, Event, Metric} from "wedding-client";

export interface Metrics {
    postEvent(event: Event): void;
    postMetric(metric: Metric): void;
}

export class MetricsPublisher implements Metrics {
    private readonly MAX_METRICS_TO_POST = 100;
    private readonly POST_METRICS_INTERVAL = 10 * 1000;

    private readonly client: Client;
    private readonly invitationId: string;
    private pendingMetrics: Metric[] = [];
    private pendingEvents: Event[] = [];
    private started: Boolean = false;
    private interval?: number = undefined;

    constructor(client: Client, invitationId: string) {
        this.client = client;
        this.invitationId = invitationId;
    }

    start() {
        if (!this.started) {
            this.interval = window.setInterval(
                (function(scope) {
                    return function(){
                        scope.flushMetrics();
                    };
                })(this),
                this.POST_METRICS_INTERVAL
            );
        }
    }

    postEvent(event: Event) {
        this.pendingEvents.push(event);
    }

    postMetric(metric: Metric) {
        this.pendingMetrics.push(metric);
    }

    getMetricsToPost = () => {
        const metricsToPost: Metric[] = [];
        const numMetrics = Math.min(this.pendingMetrics.length, this.MAX_METRICS_TO_POST);
        for (let i = 0; i < numMetrics; i++) {
            const metric = this.pendingMetrics.shift();
            if (metric) {
                metricsToPost.push(metric);
            }
        }
        return metricsToPost;
    }

    getEventsToPost = () => {
        const eventsToPost: Event[] = [];
        const numEvents = Math.min(this.pendingEvents.length, this.MAX_METRICS_TO_POST);
        for (let i = 0; i < numEvents; i++) {
            const event = this.pendingEvents.shift();
            if (event) {
                eventsToPost.push(event);
            }
        }
        return eventsToPost;
    }

    flushMetrics() {
        const metricsToPost = this.getMetricsToPost();
        const eventsToPost = this.getEventsToPost();
        if (metricsToPost.length > 0 || eventsToPost.length > 0) {
            if (window.location.host.startsWith('localhost')) {
                // Don't post metrics when running locally
                console.log('would have posted metrics ', metricsToPost);
                console.log('would have posted events ', eventsToPost);
            } else {
                this.client.postMetrics({
                    invitationId: this.invitationId,
                    metrics: metricsToPost,
                    events: eventsToPost,
                }).catch(error => {
                    console.error('error posting metrics', error);
                });
            }
        }
    };
}
```


On the server side, I used the [`@aws-lambda-powertools/metrics`](https://docs.aws.amazon.com/powertools/typescript/latest/features/metrics/) library to post metrics emitted by the server or from the client to CloudWatch using the embedded CloudWatch Logs format, to avoid synchronous latency added by calling CloudWatch APIs as part of the request. As part of this process, I discovered that the CloudWatch metrics aggregations worked a bit differently than the model I had in my head -- what I really wanted was the ability to alarm on a top-level aggregate metric, such as unhandled errors on any page on the website. If alerted, I wanted the ability to break that metric down to a list of unhandled error metrics for each page, to quickly determine what page was at issue before turning to the logs.

<a href="/assets/img/wedding/metrics-all.png" data-lightbox="metrics">
    <img src="/assets/img/wedding/metrics-all.png" alt="A screenshot of a CloudWatch metric from the AWS Console. The metric title is 'Max latency by API' and shows the 'ALL' metric selected, with individual APIs such as 'createInvitation' and 'rsvp' unselected and greyed out." />
</a>

<a href="/assets/img/wedding/metrics-by-api.png" data-lightbox="metrics">
    <img src="/assets/img/wedding/metrics-by-api.png" alt="Another screenshot of the same metric, with the previously unselected per-API metrics now visible. The ALL aggregation shows the maximum of all of these individual API latencies." />
</a>

I had actually thought that CloudWatch would do this sort of dimension aggregation automatically, but that turned out not to be true, so to achieve this I wrote a wrapper around the metrics that would automatically aggregate any metric into an `ALL` dimension, to achieve a top-level view:

```ts
public static closeMetrics(requestId: string) {
    // Create the shared metrics instance for originals + aggregates
    const metrics = new Metrics({
        namespace: 'wedding_website',
        serviceName: 'server',
    });
    // Add the original dimensions for the metric
    metrics.addDimensions(this.metricDimensions[requestId]);
    // Add the original metric values
    MetricsProvider.metricsToPublish[requestId].forEach(metric => {
        metrics.addMetric(metric.name, metric.unit, metric.value, metric.resolution);
    })
    // Publish the original metrics with their dimensions
    metrics.publishStoredMetrics();
    metrics.clearDimensions();

    // Publish aggregates by setting every key of the original dimension to a value of ALL
    Object.keys(this.metricDimensions[requestId]).forEach(dimension => {
        metrics.addDimension(dimension, 'ALL');
    });
    // Add the original metric values
    MetricsProvider.metricsToPublish[requestId].forEach(metric => {
        metrics.addMetric(metric.name, metric.unit, metric.value, metric.resolution);
    })
    // Publish the aggregated metrics with ALL dimensions
    metrics.publishStoredMetrics();
    metrics.clearDimensions();
}
```

This aggregation was expensive, but I felt it was worth it. I ended up with about 104 unique metrics across the server, website, and canary which, as I mentioned earlier, contributed to about 90% of the cost of this project.

In addition to the metrics, I wanted a way to easily see what was happening across my website that didn’t involve diving into the lambda log streams, such as the distinct Events emitted by the frontend client. I created another DynamoDB facet called an `AuditLog` which I wrote to with a record of each mutating API call, and with events submitted from the clients:

```json
{
 "LogId": "MIJMNB7LU0OOAL",
 "LogType": "RSVP_VALIDATION_ERROR",
 "Message": "Website displayed a validation error",
 "ResourceId": "MIJMMG5ACYH5U9",
 "ResourceType": "INVITATION",
 "EventData": {
  "errors": "At least one guest must be attending, otherwise please RSVP no."
 },
 "LogDay": "2025-11-29",
 "Timestamp": 1764380580207,
}
```

This would help me quickly notice any common issues that my guests were encountering and fix them proactively. As one example of where this came in useful, I noticed that there were a number of errors guests were encountering when manually logging in, and from the logs it was clear the reason why was that they were using their full house address instead of just the number (for example entering `123 Main St.` instead of just `123`), which would cause the guest lookup to fail. I was able to fix this common issue by just adding a fallback to check the first "word" in an input containing strings against the house number I had in my database:

```diff
 for (const invitation of invitationsMatchingLastName) {
     const houseNumberMatches = invitation.houseNumber.trim().toLowerCase() === input.houseNumber.trim().toLowerCase();
-    if (houseNumberMatches) {
+    const firstWordMatches = input.houseNumber.trim().includes(" ") && input.houseNumber.trim().toUpperCase().split(" ")[0] == invitation.houseNumber.trim().toLowerCase();
+    if (houseNumberMatches || firstWordMatches) {
         await UpdateInvitation.recordLogin(ClientProvider.ddb, invitation, invitation.version, Date.now());
         await CreateAuditLog.createLog(ClientProvider.ddb, {
             logId: generateId(),
```

This dropped the number of failed login events to almost zero, and would not have been as easy to discover and proactively fix without these logs showing up on my dashboard.

In addition to the ability to retrieve logs by particular resource ID (i.e. logs for a particular invitation), I wanted to be able to query Dynamo for all logs in a particular timeframe (e.g. the last 48 hours). Creating a GSI using the `LogDay` attribute allowed doing this (without creating a hot key issue) by issuing multiple Query requests for the days included in the requested timeframe, and then filtering down further in memory:

```ts
// Get all days involved in the provided range
const daysArray: string[] = [];
for (const dt = new Date(startTimestamp); dt <= new Date(endTimestamp); dt.setDate(dt.getDate() + 1)) {
    days.push(new Date(dt).toISOString().slice(0, 10)); // Add the ISO date string up to the day
}
const logs: AuditLog[] = [];
// Iterate over all days we need to retrieve from Dynamo
for (const day of daysArray) {
    // Paginate over all logs in the day's index
    let nextToken: Record<string, string> | undefined = undefined;
        do {
            const dayLogsPage: Page<AuditLog[]> = await ReadAuditLog.readLogs(ClientProvider.ddb, day, input.resourceType, input.resourceId, nextToken);
            for (const log of dayLogsPage.items) {
                if (log.timestamp >= startTimestamp.getTime() && log.timestamp <= endTimestamp.getTime()) {
                    logs.push(log);
                }
            }
            nextToken = dayLogsPage.nextStartKey;
        } while (nextToken !== undefined)
    }
```

This allowed me to build an API to efficiently retrieve logs for any arbitrary timeframe, and optionally for a specific resource:

```bash
% curl -s -X POST "https://demo.wedding/api/getAuditLogs" \
  -H ... \
  -d '{"notBeforeTimestamp": "2025-12-15T00:00:00Z", "notAfterTimestamp": "2025-12-21T18:00:00Z"}' | \
  jq -r '.results[] | [.timestamp, .logType, .resourceId, .message] | @tsv'
1766255542283	UPDATE_RSVP	MJ187UHU24NP22	RSVPs were updated for 2 guests: Thomas Becker => YES, Nancy Drew => YES
1766254347071	CLIENT_ERROR	MJ187UHU24NP22	Website client encountered an error
1766254275184	LOGIN_SUCCESS	MJ187UHU24NP22	User successfully authenticated as Thomas Becker (MJ187UHU24NP22) using lastName = Becker, houseNumber = 123
```

### Alerting

After setting up metrics, audit logs, and a canary, I needed a way to alert myself when something unexpected was happening. I signed up for PagerDuty and used its integration with CloudWatch to page me if any alarming thresholds were breached. I was really happy with PagerDuty, especially the ability to configure the paging policy to only alert me during the day and never page me overnight, and once I got all the alarm thresholds tweaked correctly, I was surprised that things were completely quiet... I should have been a bit more skeptical.

<a class="float-left" href="/assets/img/wedding/pagerduty-unauthenticated.jpg" data-lightbox="pagerduty-unauthenticated">
    <img src="/assets/img/wedding/pagerduty-unauthenticated.jpg" alt="A screenshot of the PagerDuty on iOS. The application is greyed out and a dialog box says 'Your credentials have expired or your access to the application has been revoked. Please try signing in again.'" />
</a>

After a few weeks of letting the website run in production, I opened the PagerDuty app on my phone only to find that I had been logged out of my account. I initially assumed there was some sort of expiry on the login session, which would have been annoying, however I still would have been alerted through my backup methods (email and SMS). Instead, I tried to log back in to my account and just kept getting the same message about invalid credentials.

Having flashbacks to Square disabling my account with no warning, I went to the PagerDuty website and logged in there to finally discover the issue: my “trial” had expired.

<a href="/assets/img/wedding/pagerduty-trial.png" data-lightbox="pagerduty-trial">
    <img src="/assets/img/wedding/pagerduty-trial.png" alt="A screenshot of the top of the PagerDuty dashboard. There is a banner at the top which says 'Oh no! Your trial has expired. Check out our plans to keep using PagerDuty.'" />
</a>

When you sign up for a new PagerDuty account, you are offered multiple plan options ranging from free to paid. I only needed the free functionality for my use case and never used the paid plan, but despite this, it seems that *any* new PagerDuty account is automatically enrolled in a free trial of the paid platform. When this trial expires, not only are your logged-in applications’ credentials invalidated, but your account also stops accepting any alerts from integrations until you choose not to continue with the paid features. Assuming I must have clicked something wrong when signing up for PagerDuty originally, I restarted this process with a new account and ran into the same issue, without ever utilizing any non-free features. I tried but couldn’t even pre-empt this lockout by opting out of the paid platform early in favor of the free product.

To me, this silent lockout behavior was shocking coming from an availability platform whose sole role is alerting you when something went wrong -- I would much rather just be paged to tell me that my trial had ended, and that action was required to continue coverage, than silently stop receiving alerts for an application I had already put into production. I reported this sharp edge to PagerDuty via their feedback page in September of 2025, and as of posting this it doesn’t seem to have been addressed. Although I would recommend PagerDuty once you’re fully onboarded, this is an extremely dangerous sharp edge which urgently needs fixing in my opinion.

A funny thing that happened to me as a result of having this paging setup which monitored my service running on AWS, while also working at AWS, was that I happened to be on-call for our team in EC2 during the recent [DynamoDB event in us-east-1](https://aws.amazon.com/message/101925/), and started receiving pages from both our internal monitoring systems and my wedding website:

<a href="/assets/img/wedding/wedding-page.png" data-lightbox="wedding-page">
    <img class="tall-image" src="/assets/img/wedding/wedding-page.png" alt="A screenshot of two critical notifications on the iOS lockscreen, one is from the Amazon paging app and the notification text is redacted, while the other is from PagerDuty and states that the 5xx error rate for the wedding website has breached the threshold." />
</a>

Needless to say, I knew which of those alerts took priority, but I was happy at least to see that my monitoring was working correctly!!

## Going Live

After working through all these details and getting the website finished, tested, and properly monitored, I was more than ready for some work on the human side of this project! Putting our RSVP vision into action was enabled using the [`@react-pdf/renderer`](https://www.npmjs.com/package/@react-pdf/renderer) library, which allowed me to generate a printable file with the individualized QR codes for each recipient. I color and font-matched these with the invitations themselves, which we designed and ordered on [Minted](https://www.minted.com) (which we LOVED and cannot say enough good things about). I included some tiny text at the top of each RSVP card so that we could match the recipient with their envelope. The end result was a sleek experience both visually and technically.

<a href="/assets/img/wedding/rsvp-sheets.png" data-lightbox="rsvp-sheets">
    <img src="/assets/img/wedding/rsvp-sheets.png" alt="A screenshot of the Preview app on MacOS, showing a PDF open. The PDF contains multiple of the previously seen QR code inserts for the invitations, with small names of the invitees at the top and dotted lines for cutting." />
</a>

### Admin console

While eagerly awaiting the responses from our guests, I built us some protected admin pages into the website to track the progress of our responses, and to be able to export the data we and our vendors needed, such as meal choices and wedding gift details.

<div class="gallery">
  <div class="gallery-item">
    <a href="/assets/img/wedding/admin-invitations.png" data-lightbox="admin-gallery">
      <img src="/assets/img/wedding/admin-invitations.png" alt="A screenshot of the admin page on the wedding website, showing all of the invitations to the wedding. People who have RSVP'd yes are highlighted in green, and there are counters on the top to show how many responses are outstanding." />
    </a>
    <div class="desc">A view of all the invitations and who has responded</div>
  </div>
  <div class="gallery-item">
    <a href="/assets/img/wedding/admin-guests.png" data-lightbox="admin-gallery">
      <img src="/assets/img/wedding/admin-guests.png" alt="Another screenshot of the admin page, this time showing each guest's RSVP, their meal choice, and any dietary restrictions" />
    </a>
    <div class="desc">A view of each guest, their RSVP, and meal preferences</div>
  </div>
</div>

## One Last Hurrah

After our incredible wedding went off without a (serious) hitch, we jumped on a plane for our honeymoon, and then returned to reality, I felt a growing hole in my heart. I really loved building this website, and I am so proud of how it turned out. Working on something so personal gives me a reason to care deeply about the small details, which is something I love to do. I came up with one last opportunity to build something tailored and fun.

I coded up a rickety but working photo-tagging interface built on [Yet Another React Lightbox](https://yet-another-react-lightbox.com) and [React Photo Album](https://react-photo-album.com) that could be used to tag the photos we got back from our photographer to the invitations in Dynamo. I experimented with using facial recognition libraries to accelerate this process, but found that it was just unreliable enough that its result would require a manual review anyways, and it missed some people who were obvious to us as humans who remembered what people were wearing and who was together. My plan was to allow people to filter photos on the website to just the ones with them in it, so I wasn’t okay with any false-positives or misses of really good photos of them that just happened not to get auto-tagged. My wife and I put on a terrible reality TV show (Love is Blind...) got through tagging each of the 1,000+ photos before the season was over.

As a result of this work, I was able to replace our home page with a nice photo gallery experience that we sent back out to our guests so that they could relive the memories, and also have the opportunity to upload and share their own with us:

<div class="gallery">
  <div class="gallery-item">
    <a href="/assets/img/wedding/album-all.png" data-lightbox="album-gallery">
      <img src="/assets/img/wedding/album-all.cropped.png" alt="The homepage of the website once authenticated, shows a photo of the couple and a countdown timer to the wedding day." />
    </a>
    <div class="desc">The whole photo album</div>
  </div>
  <div class="gallery-item">
    <a href="/assets/img/wedding/album-tagged.png" data-lightbox="album-gallery">
      <img src="/assets/img/wedding/album-tagged.png" alt="The 'Location' page of the website, shows information about the venue, the wedding day schedule, transportation and lodging options, and things to do while in town." />
    </a>
    <div class="desc">A separate section for just the tagged photos of the guest</div>
  </div>
</div>

## In Conclusion

Out of everything I did, there was really only one mistake in hindsight -- I should have asked for people’s email addresses when RSVPing. We had their street addresses, obviously, but no way to easily communicate any reminders or updates to our guests who indicated they would be attending. Luckily this didn’t end up being too big of an issue, but if I were doing this over again I would absolutely fix that and require an email address from everyone who indicated they were coming.

I **really** had fun with this project and am sad that it’s now come to an end. I wrote this post as much to brag about all the work I put into this as to prolong the end of this story just a bit longer.

As silly as it may seem, this is what software engineering is all about to me -- I love being able to bring just about any experience I can think of in my head to fruition, and have an impact on my life and others’. I love all the complexity and intentional decisions that sometimes underlies something that seems so simple and works well. I also am a firm believer that anything worth doing is worth overdoing, especially when it comes to something so meaningful and personal as my wedding.

And although it may seem like I spent an exorbitant amount of time on this project in the midst of such an important time for planning (and I did), I am also a believer in balance, and in sharing the load. Throughout this process my wife and I planned our wedding as a team while playing to our strengths -- sometimes that involved me leaving some website ideas on the cutting room floor and making sure the actually-important things were done first. But I feel thankful that my partner saw how much joy this brought me and supported me 100% in this mostly completely unnecessary exercise in overdoing something.

<div class="center">
    <img class="tall-image" src="/assets/img/wedding/wedding-pic.jpg" alt="A photo of our doggy at the wedding :)" />
</div>