> **»The only stupid question is the one that is not asked.«**  
> *– Hull, E., K. Jackson, et al. (2005).*

## What is Wekan?
As already explained in detail in our [Readme][], Wekan is an open-source _[kanban board][kanban]_ that lets you organize things in cards, and cards in lists.

[readme]: https://github.com/wekan/wekan/blob/master/README.md
[kanban]: https://en.wikipedia.org/wiki/Kanban_board

## Weren't you called Libreboard before?
Yes, Libreboard was the old project name, which superseded the even older project name Metrello. As the original name suggests, Metrello was a Trello clone built with Meteor. It used a lot of the original assets from Trello and even the name was very similar. When the project turned more mature and gained more interest by the community, this was obviously a [problem]. To get it's own identity and due to a DMCA from Trello, efforts started to [redesign] Metrello, which also included to find a new name and so Maxime Quandalle came up with “OpenBoard”, to underline the open source nature of the project. Unfortunately the com domain was already taken and so she replaced the Open with Libre, which stands for free (as in freedom) in many Latin derived languages.

After renaming it to Libreboard, a [new logo] was designed and the project continued to live on as Libreboard. Unfortunately it turned out, that the new logo was apparently ripped-off from a [concept] published at Dribbble, and so a new logo had to be found. There were a lot of [ideas from the community][logo-ticket], and at the end Maxime [proposed][wekan-proposal] a completely new name, Wekan, together with a design proposal for a new logo.

[problem]: https://github.com/wekan/wekan/issues/92
[redesign]: https://github.com/wekan/wekan/issues/94
[new logo]: https://github.com/wekan/wekan/issues/64#issuecomment-69005150
[concept]: https://dribbble.com/shots/746215-Pigeon
[logo-ticket]: https://github.com/wekan/wekan/issues/64#issuecomment-74357809
[wekan-proposal]: https://github.com/wekan/wekan/issues/64#issuecomment-135221046

## What is the difference between Wekan and Trello?
The main difference between the two is that Wekan is completely open source and available under the permissive MIT license. That makes it possible to host it on your own server (or your company's or organization's server) and you keep the full control over all data. No need to fear it will disappear some day, like a commercial service like Trello could.  
Additionally the long term goal is to have features that are not available on Trello or other alternative, making Wekan flexible and suitable for complex project organizations.

## Why does Wekan looks so different now compared to < v0.9?
Wekan started as a just for fun project to explore meteor and it's features and the initial version had a lot of the Trello assets (CSS, Images, Fonts) in it and copied a lot of it's design. Due to an DMCA takedown notice and obviously to get its own identify, the old design was dropped after v0.8 and a new UI was developed

See the related tickets [#92] and [#97] for more information.

[#92]: https://github.com/wekan/wekan/issues/92
[#97]: https://github.com/wekan/wekan/issues/97

## How can I connect to the Wekan DB?
If you're using Docker images. Wekan is configured to use MongoDB, by using a **separate** mongo Docker image / container. After you start the Docker images (`docker-compose up -d`), you can list the containers via:
```sh
docker ps
```
Then, find the MongoDB image (with the container name: `wekan_wekandb_x`). Remember the _Container ID_. And connect to the running container:
```sh
docker exec -i -t <container_id> /bin/bash
```
Finally, connect to the Wekan database:
```sh
mongo wekan 
```
List the tables:
```sh
show collections
```
List all users:
```sh
db.users.find()
```

## Show mails with a Docker image, without mail configuration
When you did **NOT** setup the `MAIL_URL` environment variable in Wekan, the mail message will be 'sent' to the terminal output instead of sending an actual e-mail. If you are using Docker images, list the containers via:

```sh
docker ps
```

Then attach to the process:

```sh
docker attach --sig-proxy=false <container_id>
```

With the `--sig-proxy=false` flag, you can close the attached shell again via **ctl + x** without exiting the Wekan process.

Via the web-interface press the '_forgot your password?_' link and trigger a reset mail. And watch the terminal output for the e-mail.

## How can I contribute to Wekan?
We’re glad you’re interested in helping the Wekan project! We welcome bug reports, enhancement ideas, and pull requests, in our GitHub bug tracker. Have a look at the [Contributing][] notes for more information how you can help improve and enhance Wekan.

[contributing]: https://github.com/wekan/wekan/blob/master/Contributing.md