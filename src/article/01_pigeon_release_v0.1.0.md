# Pigeon Release v0.1.0: Open source email automation written in Rust

I found that email automation solutions like Mailchimp or ConvertKit are quite expensive. I was using Pigeon for my projects already a while ago, but figured it could be more useful as an open source project.

[Pigeon](https://github.com/quambene/pigeon-rs) is a command line tool based on the excellent libraries [clap](https://crates.io/crates/clap), [connectorx](https://crates.io/crates/connectorx), and [polars](https://crates.io/crates/polars).

Using clap, it is super easy to create a command line tool. Everything just boils down to a `match`ing exercise for all subcommands and command line arguments. Rust's `Option` shows its full power here. Et voilà, after hardcore `match`ing for a few hours, you will be gifted with a stable and production-ready application.

Let's take a look how you could use pigeon. For example, Pigeon queries all subscribers of your newsletter, creates a plaintext and html email from a template file, and delivers it to all of them:

``` bash
pigeon send-bulk \
    sender@your-domain.com \
    --receiver-query "select email from user where newsletter_confirmed = true" \
    --message-file "message.yaml" \
    --display \
    --assume-yes
```

Console output:

``` bash
> Display query result: shape: (4, 1)
+------------------------------+
| email                        |
| ---                          |
| str                          |
+==============================+
| "marie@curie.com"            |
+------------------------------+
| "alexandre@grothendieck.com" |
+------------------------------+
| "emmy@noether.com"           |
+------------------------------+
| "elie@cartan.com"            |
+------------------------------+
> Sending email to 4 receivers ...
marie@curie.com ... ok
alexandre@grothendieck.com ... ok
emmy@noether.com ... ok
elie@cartan.com ... ok
```

The database query is achieved via connectorx. I like the way how you get type safety but without having to define the types yourself. At first, connectorx queries a single row to convert the postgres/mysql/etc. schema to the corresponding Rust types. Then, the query result will be downloaded the Rust way: fast, efficient, and gentle to your RAM.

You could also get the relevant emails from a csv file using `--receiver-file` instead of `--receiver-query` in the command above. In both cases, the tabular data is handled with polars which is the Rust equivalent of Python's pandas for handling `DataFrames`. As an additional benefit, polars displays the tabular data in a clearly arranged way to your console.

Now let's assume you want to personalize your emails. You can use Pigeon's `--personalize` to achieve this:

``` bash
pigeon send-bulk \
    albert@einstein.com \
    --receiver-query "select first_name, last_name, email from user where newsletter_confirmed = true" \
    --message-file "message.yaml" \
    --personalize "first_name" "last_name" \
    --display
```

Console output:

``` bash
> Display query result: shape: (4, 3)
+-------------+----------------+------------------------------+
| first_name  | last_name      | email                        |
| ---         | ---            | ---                          |
| str         | str            | str                          |
+=============+================+==============================+
| "Marie"     | "Curie"        | "marie@curie.com"            |
+-------------+----------------+------------------------------+
| "Alexandre" | "Grothendieck" | "alexandre@grothendieck.com" |
+-------------+----------------+------------------------------+
| "Emmy"      | "Noether"      | "emmy@noether.com"           |
+-------------+----------------+------------------------------+
| "Elie"      | "Cartan"       | "elie@cartan.com"            |
+-------------+----------------+------------------------------+
> Display message file: MessageTemplate {
    message: Message {
        subject: "Issue No. 1",
        text: "Dear {first_name} {last_name},
            Welcome to my newsletter. We are doing hard sciences here.
            Sincerely, Albert Einstein",
        html: "Dear {first_name} {last_name},
            Welcome to my newsletter. We are doing hard sciences here.
            Sincerely, Albert Einstein",
    },
}
> Display emails: BulkEmail {
    emails: [
        Email {
            sender: "albert@einstein.com",
            receiver: "marie@curie.com",
            message: Message {
                subject: "Issue No. 1",
                text: "Dear Marie Curie,
                    Welcome to my newsletter. We are doing hard sciences here.
                    Sincerely, Albert Einstein",
                html: "Dear Marie Curie,
                    Welcome to my newsletter. We are doing hard sciences here.
                    Sincerely, Albert Einstein",
                },
        },
        Email {
            sender: "albert@einstein.com",
            receiver: "alexandre@grothendieck.com",
            message: Message {
                subject: "Issue No. 1",
                text: "Dear Alexandre Grothendieck,
                    Welcome to my newsletter. We are doing hard sciences here.
                    Sincerely, Albert Einstein",
                html: "Dear Alexandre Grothendieck,
                    Welcome to my newsletter. We are doing hard sciences here.
                    Sincerely, Albert Einstein",
            },
        },
        Email {
            sender: "albert@einstein.com",
            receiver: "emmy@noether.com",
            message: Message {
                subject: "Issue No. 1",
                text: "Dear Emmy Noether,
                    Welcome to my newsletter. We are doing hard sciences here.
                    Sincerely, Albert Einstein",
                html: "Dear Emmy Noether,
                    Welcome to my newsletter. We are doing hard sciences here.
                    Sincerely, Albert Einstein",
            },
        },
        Email {
            sender: "albert@einstein.com",
            receiver: "elie@cartan.com",
            message: Message {
                subject: "Issue No. 1",
                text: "Dear Elie Cartan,
                    Welcome to my newsletter. We are doing hard sciences here.
                    Sincerely, Albert Einstein",
                html: "Dear Elie Cartan,
                    Welcome to my newsletter. We are doing hard sciences here.
                    Sincerely, Albert Einstein",
            },
        },
    ],
}
> Should an email be sent to 4 recipients? Yes (y) or no (n)
>
```

That's it. Pigeon has some more handy features which you can check out on [github](https://github.com/quambene/pigeon-rs) and it is on [crates.io](https://crates.io/crates/pigeon-rs) as well.

Currently, Pigeon is based on AWS Simple Email Service as email provider which is why it is quite cheap to use. The following table compares the price per month for email provider and emails per month:

&nbsp; | 5,000 | 10,000 | 100,000
--- | --- | --- | ---
**Pigeon+**[**AWS**](https://aws.amazon.com/ses/pricing/) | $4.50 | $5 | $14
[**Mailchimp Marketing**](https://mailchimp.com/pricing/marketing/) | $9.99 | $20.99 | $78.99
[**Mailchimp Transactional**](https://mailchimp.com/pricing/transactional-email/) | - | - | $80
[**Sendgrid Marketing**](https://sendgrid.com/pricing/) | $15 | $15 | $120
[**Sendgrid API**](https://sendgrid.com/pricing/) | $14.95 | $14.95 | $29.95
[**ConvertKit**](https://convertkit.com/pricing) | $66 | $100 | $516

Currently, you have to connect your database and your email provider via environment variables which is not quite user-friendly. It's working for me quite well, but I would be interested in your feedback for potential improvements.

Edit: Polars is not exactly the Rust equivalent of Python's pandas. There is a Python version of polars, too. [Here](https://h2oai.github.io/db-benchmark/) is a benchmark for both.

_First published on [Reddit](https://www.reddit.com/r/rust/comments/qy85sg/pigeonrs_open_source_email_automation_written_in/) (2021-11-20)._
