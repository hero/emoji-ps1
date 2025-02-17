# Emoji Command Prompt 💻
![Kapture 2021-08-30 at 20 10 05](https://user-images.githubusercontent.com/2320747/131357413-7e8921de-e70c-4a27-84af-cb74e943aad3.gif)
> ### [Blog post](https://bigomega.medium.com/adding-emojis-to-your-command-prompt-and-animate-it-7884355fd54d)

**Table of Contents**
- [Emoji Command Prompt 💻](#emoji-command-prompt-)
  - [:package: Installation](#package-installation)
    - [ With OhMyZsh](#-with-ohmyzsh)
    - [ Without OhMyZsh](#-without-ohmyzsh)
  - [:drum: Features \& Customization :hammer\_and\_wrench:](#drum-features--customization-hammer_and_wrench)
    - [:spiral\_calendar: Schedule](#spiral_calendar-schedule)
    - [🎮 Animation](#-animation)
    - [🦾 Automating animations](#-automating-animations)
    - [✅ Finishing tasks](#-finishing-tasks)
  - [🍻 Contribution \& Request](#-contribution--request)
  - [🎫 License](#-license)

## :package: Installation
```sh
# Clone the repo
git clone git@github.com:bigomega/emoji-ps1.git
cd emoji-ps1
```
`cd`-ing into the repo is inmportant because we'll be using `$PWD`
### <img src="https://user-images.githubusercontent.com/2320747/131363393-c2f28fdf-7675-49f2-bc8a-42b62936a877.png" width="20px"/> With OhMyZsh
This is written on top of the [robbyrussell](https://github.com/ohmyzsh/ohmyzsh/wiki/Themes#robbyrussell) (default) theme.
```sh
# Link it to the custom themes folder
cp emoji.js $HOME/.oh-my-zsh/custom/themes/emoji.js
cp emoji.zsh-theme  $HOME/.oh-my-zsh/custom/themes/emoji.zsh-theme
# or
cp emoji.* $HOME/.oh-my-zsh/custom/themes/
```
Set the theme in `~/.zshrc` file
```sh
ZSH_THEME="emoji"
```
### <img src="https://user-images.githubusercontent.com/2320747/131363393-c2f28fdf-7675-49f2-bc8a-42b62936a877.png" width="20px"/> Without OhMyZsh
For a simple version
```sh
# Prepending emoji to the current PS1
echo "\n#Emoji PS1\nPS1=\"\\\$(node $PWD/emoji.js) \"\$PS1" >> ~/.bashrc
source ~/.bashrc
```
For animations, copy the [`psanimate` and `psanimate_stop` functions](https://github.com/bigomega/emoji-ps1/blob/33a1318e95cbcffa64757144849a46043409a79a/emoji.zsh-theme#L22-L52) from the `/emoji.zsh-theme` file to `~/.bashrc`
> If you face issues with node, install/update node to the latest stable version. This was developed on `v16.6.0`

## :drum: Features & Customization :hammer_and_wrench:
### :spiral_calendar: Schedule
The `emoji.js` file contains the logic behind the what emoji to show and when.
There's a Schedule for the emoji which you can/should change in JS [here](https://github.com/bigomega/emoji-ps1/blob/33a1318e95cbcffa64757144849a46043409a79a/emoji.js#L10-L21).
```js
const timings = [
  // from, duration, emoji, highlight?, unstoppable?
  [0, 500, '🛌', true, true],
  [530, 200, getRandom(activity_list)],
  [800, 200, '🥪', true],
  [1300, 130, '🍛', true],
  ...
```
The `highlight` flag shows an arrow ` ⬅` after the emoji
<img width="1123" alt="Screenshot 2021-08-30 at 21 33 31" src="https://user-images.githubusercontent.com/2320747/131369199-3f87ad67-dd0e-4726-a044-e472312ee157.png">
The `unstoppable` flag says that the scheduled emoji cannot be overridden by

You can/should edit these two lists as well depending your interests, likes and visually appealing emojis.
```js
const fun_list = "👾,🍀,🥑,⛰️ ,🪂,🍺,👨🏻‍🌾,🐢,🐼,🐙,🐳,🐓,🪵 ,🍄,🔥,🌪 ,🍁,🐚,🌊,🍉,🥝,🍋".split(',')
const activity_list = '🎨,🦮,📚,✍️ ,🎸,🛹,🏃🏻‍♂️'.split(',')
```
### 🎮 Animation
All of these could be animated. You can start the animation with the command (bash function) `psanimate <interval-in-seconds>`, defaults to 1 second. Animate calls the emoji function in the given interval with a rotating SWITCH boolean.
![Kapture 2021-08-30 at 22 05 28](https://user-images.githubusercontent.com/2320747/131373246-d075b3fe-1ba5-4409-932c-15bc4e3a0847.gif)

The following is dinner-time highighted emoji with `psanimate .2`
![Kapture 2021-08-30 at 21 58 12](https://user-images.githubusercontent.com/2320747/131372343-7e7d6060-a96f-4d1f-8adb-d66ea5c63168.gif)
> Animation runs as a background process, stores the pid in `/tmp/psanimatepid-$$`.
### 🦾 Automating animations
This is disabled by default since automated animations could be very much annoying. But you can enable it by setting the `PS_AUTO_ANIMATE` variable. The schedule and check-interval is in the function right below the variable. By default it checks every 30 minutes and animates during sleep time.
```bash
PS_AUTO_ANIMATE=1
```
### ✅ Finishing tasks
Certain activity emojis like food can be overridden (when it's over). This can be done with the command `pstaskover`. This [sets the env](https://github.com/bigomega/emoji-ps1/blob/33a1318e95cbcffa64757144849a46043409a79a/emoji.zsh-theme#L12) variable `PS_TASK_OVER` and so an emoji from the `fun_list` is picked up after.
![Kapture 2021-09-03 at 12 29 52](https://user-images.githubusercontent.com/2320747/131964014-d717b0ae-c1f9-4b88-88b2-8d6780c85ef6.gif)
> The PS_TASK_OVER resets after an hour. It uses bash traps.
## 🍻 Contribution & Request
If you find this idea interesting or if you can imagine beautiful ideas, please send a PR or raise a request for it. Thanks 🙏

## 🎫 License
[MIT](https://github.com/bigomega/emoji-ps1/blob/c27073e9241ae2f1386dd6898fadf3619179a7e2/LICENSE) © [bigomega](https://github.com/bigomega)
