## Creating a generative track

In the summer of 2022, I took UC Berkeley's Music 158A: Music and Computing with CNMAT Technologies. For my final project, I set out to synthesize a convincing harp sound in Max/MSP. I didn't quite get there, but I did like the sounds I created, so I used some other tools I learned in the class to create some generative music. This is a breakdown of that process.

<video src='videos/fullaudio.mp4' width='100%' height='50px' controls></video>

## Synthesis

### Karplus-Strong
I started with an algorithm called Karplus-Strong to model my harp strings. 

(Karplus-Strong)[images/karplus-strong.png]

It works by taking an input signal (`in1`), usually a burst of noise, and putting it through a delayed feedback loop. The frequency of the output (`in2`) is determined by the amount of delay: smaller delays correspond to higher frequencies. The diagram above is an implementation of the feedback loop in Gen, a low-level Max extension that operates on samples.

As is, in this system low frequencies will die out slower than high frequencies. This is because the scaling factor we choose (0.97 in this case) will be applied more often with a shorter delay times, so the output signal decays faster.

(Karplus-Strong)[images/karplus-strong2.png]

We address this above by changing the gain based on amount of delay. 
Above we introduce a new input, ('in3'), to represent decay in seconds. Multiplying that by frequency (Hz), gives us the number of delays, or multiplcations, that will happen in the time we want the signal to decay. Gen's `t60` object outputs a multiplication factor that, when applied sample by sample, will cause a signal to reduce in amplitude by 60 dB. So, we can use this object to choose the feedback gain in a way that will decay any frequency at the same rate. 

<video src='videos/karplus-basic.mp4' width='100%' controls></video>

To test out this karplus-strong implementation, I 

### Markdown

Markdown is a lightweight and easy-to-use syntax for styling your writing. It includes conventions for

```markdown
Syntax higlshlighted code block

# Header 1
## Header 2
### Header 3

- Bulleted
- List

1. Numbered
2. List

**Bold** and _Italic_ and `Code` text

[Link](url) and ![Image](src)
```

For more details see [Basic writing and formatting syntax](https://docs.github.com/en/github/writing-on-github/getting-started-with-writing-and-formatting-on-github/basic-writing-and-formatting-syntax).

### Jekyll Themes

Your Pages site will use the layout and styles from the Jekyll theme you have selected in your [repository settings](https://github.com/bcylincoln/spaceharps/settings/pages). The name of this theme is saved in the Jekyll `_config.yml` configuration file.

### Support or Contact

Having trouble with Pages? Check out our [documentation](https://docs.github.com/categories/github-pages-basics/) or [contact support](https://support.github.com/contact) and we’ll help you sort it out.
