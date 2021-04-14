# WORKFLOW FOR GOOGLE/FONTS REPO

This workflow is meant to not lose product in the publishing process, to make checking easier, and finally to keep people updated of the status of their project. Indeed the persons implicated with the google/fonts repo are working remotely from different timezones and sometimes not even knowing each others. It seemed also important to avoid the multiplication of apps to organize the worklow, and to keep all in one place — mostly to avoid copy-pasting PR's links all the time.

### [GITHUB PROJECTS](https://github.com/google/fonts/projects)
PRs and Issues are monitoring in 2 differents github projects. Then, each font engineers contracted by GF have a personal board to manage their own project. Then we gladly use labels to make commication more efficient within the team, and to help reminding the content of the issues/PRs. I tried to categorize the labels title using prefixes, significant colors and definitions (this is still in progress though, I haven't finished sorting the issue tracker). Dave can assign people direclty to issues and PRs, or font engineers can assign themselves if they want to complete their priority line.

#### ISSUES
The **[Pipeline Overview](https://github.com/google/fonts/projects/7)** project is initially meant to be managed by Dave. This is still widely a construction site since I first focus on sorting the PRs.

The idea is to categorize the issues between:
- **New font submissions**: non curated list of issues suggesting open source fonts to add to the catalog
- **On board to do list**: selection of fonts to on board
- **Axis registry related discussions**
- **Fix to do list**: selection of issues requiring to fix a fonts
- **Update to list**: selection of fonts which have been updated upstream

![Pipeline Overview](https://user-images.githubusercontent.com/12222436/104586226-7e903e00-5665-11eb-911b-17c1ab433baa.png)

This should give a first sorting of what is relevant to look in the long and wild list of issues. Then, they can be attached to Milestones to give a better prospect view, and we can add labels directly to the issues to give more details about the job. 

For the time being, the Milestones and the Pipeline Overview are redundant and unsynchronized. IMO we should either stop using one, or find a way to make them complementary. For eg. Milestones could have a timeline (with not-too-ambitious and regularly-updated quaterly goals), and only contains issues that are meant to be solved short terms — backlog being in the Pipeline Overview. 

In a second time, I plan to create templates for issues to help users in defining them and spare us some research time.

### PRs
The **[Traffic Jam](https://github.com/google/fonts/projects/1)** project is managed by me. It is meant to follow PR from submission to publication, knowing that its content is supposed to be pushed to 3 different servers: the developper sandbox, the sandbox, and finally Google Font API. 

![Traffic Jam Board](https://user-images.githubusercontent.com/12222436/104586245-851eb580-5665-11eb-8288-0e486c0399ab.png)

Font engineers submit a PR which is then reviewed by Marc and/or me on Tuesdays and Wenesdays. According to the result of this review, the PR is merged or not. The columns of Traffic Jams indicates the PR status and in which server the PR stands. Even though these columns exists, I created redundant labels (to sandbox, to production, live) to allow engineers to be aware of the PR status without checking Traffic Jam, or to have a good overview just by looking at the PR section.

#### PR checking process
1. When a PR is submitted, it should be placed in the Traffic Jam project. It goes directly to the collumn "Pending". At least 2 labels should be added: a category (new, upgrade, fix…) and a status (in progress, ready for review…). The author of the PR should take the habit of doing so to facilitate communication with the reviewer.

![PR Example](https://user-images.githubusercontent.com/12222436/104586334-9ff12a00-5665-11eb-8d83-0de3938efcb0.png)
*—This can be done directly in the PR*

2. Then Marc and/or I check the QA the content of PR to validate it or not. The status label is updated accordingly (Ready to push, need upstream resolution, regresion…).
3. When it is merged, it goes automatically in the column "In transit". Then, we should check the font in the dev sandbox, but it is often buggy tbh. If the product is well displayed with no errors or bugs, it can go to Sandbox: we add it to the [to_sandbox.txt file](https://github.com/google/fonts/blob/main/to_sandbox.txt). If not, it is blocked, ie a new PR is needed to fix it. 
4. Once or every 2 weeks, an API engineer is checking the to_sandbox list, and push the list to Sandbox. Once done, Marc and/or I check manually if the font (or the designer information etc.) appears in Sandbox, and if it is working correctly. If yes, it can be added to the [to_production.txt file](https://github.com/google/fonts/blob/main/to_production.txt). If not, it is blocked, ie a new PR is needed to fix it.
5. Once or every 2 weeks, an API engineer is checking the to_production list, and push the list to GF API. Once done, Marc and/or I check manually if the entire list got through and display correctly.

In order for the process to be transparent and efficient, we add the labels below.

#### Category
- **New Font**: Font or a font family addition
- **Upgrade**: multiple fixes, upgrade or VF replacement
- **Fix**: small fix(es) which doesn't need much communication
- **Description/Metadata/OFL**: Modification in a font directory but not the font itself (ie. html snippet or METADATA.pb)
- **Catalog**: Designer's information
- **Axis Registry**: variable axes registration related stuff

#### Status before merging
- **In Progress**: engineer is working on it
- **Upstream is working on it**: designer is working on it
- **Ready for review**: PR is ready to be review for validation and merging

#### Result of review
- **Need Upstream Resolution**: upstream fix required
- **Regression**: Diff against previous published version (v-metrics, weight…)
- **Ready to push**: can go to sandbox
- **Needs Meta/Description changes**: Metadata.pb or html snippet need corrections

#### Status after merging
- **Blocked**: blocked once merged, has to be fixed with new PR
- **to_sandbox**: PR merged, can be added to [to_sandbox.txt](https://github.com/google/fonts/blob/main/to_sandbox.txt) will be visible in Sandbox within 1-2 weeks
- **In sandbox**: Visible in sandbox
- **to_production:** Ready for publication, can be added to [to_production.txt](https://github.com/google/fonts/blob/main/to_production.txt), will go to prod within 1-2 weeks
- **Live:** Published!

#### Other
- **Needs confirmation**: Needs an answer from upstream, engineer, or management to be able to move foward
- **Need Dave's opinion**: Daves need to answer this

#### PERSONAL BOARDS
Let's take the example of my board: **[Rosa's Roadmap](https://github.com/google/fonts/projects/3)**. The board shows issues related to each project (one font = one issue. 

![Rosa's Roadmap](![Uploading Capture d’écran 2021-04-14 à 18.32.44.png…])

You can access a lot of the issue's informations from the board. Particularly the first comment, in which you can add the link to the upstream repo and a to-do list to keep an archive of the progress of the project. When a PR is opened, we need to link it to its related issue: then the board is automated to move the issue from "in progress" to "done" when the PR is merged.

![Issue pannel from the board](https://user-images.githubusercontent.com/12222436/114746522-28a86080-9d50-11eb-9a77-7415cfaa08f5.png)

These boards are of course useless if they are not updated reguarly.


#### PERSONAL THOUGHTS ON STUFF WE CAN'T REALLY RESOLVE FOR NOW

The prohibition of using third-part plug-in to improve the github projects makes this workflow more laborious than it could. Manual stuff could be spared thanks to some plugins — like the interaction between different project boards. It could also help to improve clarity and readability.

Finally, the fact that google/fonts repo is watched by a large audience leads to people commenting our actions in a regular basis. Some interventions are welcome and are actually helping, but most of the time it is making our work a bit more harder and the space of a bit more unsafe. After discussing with the team we thought it would be a good idea to create a "code of conduct" where it could be explained that google/fonts is actually a workspace and therefore needs to be respected as such.
