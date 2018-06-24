[![Try on Sandstorm][sandstorm_button]][sandstorm_appdemo]

[Wekan for Sandstorm Install/Download](https://apps.sandstorm.io/app/m86q05rdvj14yvn78ghaxynqz7u2svw6rnttptxx49g1785cdv1h)

[Sandstorm](https://sandstorm.io)

[Building Wekan for Sandstorm](https://github.com/wekan/wekan-maintainer/wiki/Building-Wekan-for-Sandstorm)

[Sandstorm Board not Found error](https://github.com/wekan/wekan/wiki/Export-from-Wekan-Sandstorm-grain-.zip-file)

[Wekan Sandstorm cards to CSV using Python](https://github.com/wekan/wekan/wiki/Wekan-Sandstorm-cards-to-CSV-using-Python)

It is not possible to import attachments directly from Trello when using Sandstorm version of Wekan. This is because Wekan is in secure sandbox at Sandstorm, and does not yet have Sandstorm-compatible way to import attachments from outside of Sandstorm. You need to:
1. Install Standalone version of Wekan, for example Docker/Snap/VirtualBox, for example to your own computer
2. Import board from Trello
3. Export board as Wekan board. Exported JSON file includes attachments as base64 encoded files.
4. Import board as Wekan board to Sandstorm.
