![Hat Guide Step 1](../../assets/HatGuide/HatGuide1.png)



Important Rules:
Players should be submitting both a hat and the icon for approval. 
Players should also not be submitting images without first having a hat token available. 

🟥 🟥 🟥 WARNING 🟥 🟥 🟥
Exercise caution in uploading certain gif hats as they may crash the server

1) Press F11 and navigate to "Manage Uploads"  [refer to first image]

2) Keep that hat window open and navigate to your RC & open up classes [refer to second image]

3) From classes hit ctrl+f and search for items_hat and use the latest hat class and double click to open [refer to third image]

4) Locate the Player Hat Tokens line and start below the last entry and follow the previous format [refer to fourth image]
(Example: this.72974= {"n", "name of token, "icon-image.png", "Hat", 0, 0, "theEntireImageName.png"};   this.72974.prop.cantDrop = true;) 

5) Confirm that the item i.d. you create is currently not in use by going to your RC and typing in the command /npc iteminfo (ID #)  [refer to fifth image]

6): Once confirmed not in use navigate back to the F11 upload and hit "approve" for both the hat and the icon

7) Hit apply and confirm that the database was updated in RC [refer to sixth image]

8) Test that the hat works by using the command :seth <id #> 

Troubleshooting tips:
To make sure the images are working you can also place down a block and type :i <image name> to see if it's successfully uploaded in the game 
