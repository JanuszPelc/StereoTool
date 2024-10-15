## JP Stereo Tool

A native device for Bitwig Studio that fills a gap in its metering options.

Primarily functioning as a stereo balance and phase correlation meter, it helps maintain well-balanced mixes and identify mono compatibility issues.

Additionally, it offers a few controls for shaping the stereo image, enhancing its utility in everyday music production and sound design tasks.

![User Interface Overview](https://github.com/JanuszPelc/StereoTool/raw/main/Assets/Images/Overview.png)

The default **Metering View** provides a streamlined monitoring interface:

1. **Balance Meter**: Indicates the perceived center position (balance) within the stereo field.
2. **Correlation Meter**: Displays how well the left and right channels are aligned (phase correlation).
3. **Knob List**: Toggles between the **Metering View** and the **Control View**.

The **Control View** offers access to stereo shaping controls:

4. **Stereoize Knob**: Adds extra stereo content to a mono or stereo signal (stereo enhancement).
5. **Width Knob**: Adjusts the width of a stereo signal (side loudness).
6. **Panning Knob**: Shifts the signal's position within the stereo field (true stereo panning).
7. **Meters Knob**: Adjusts the responsiveness of the meters' movement (average measurement time).

## How to Install

The [GitHub repository](https://github.com/JanuszPelc/StereoToolTest) for **JP Stereo Tool** contains all releases, as well as documentation and license information.

1. Visit the repository's [Latest Release](https://github.com/JanuszPelc/StereoToolTest/releases/latest) page to download the "JP-Stereo-Tool-Download.zip" file.
2. Unzip the downloaded file to access the "JP Stereo Tool.bwpreset" file.
3. Drag and drop the "JP Stereo Tool.bwpreset" file onto a track in Bitwig Studio's arrangement or mixer window.
4. In Bitwig Studio, right-click on the device you just added and select "Save Preset to Library" to make it easily accessible later.

Alternatively, you can copy the downloaded "JP Stereo Tool.bwpreset" file directly into Bitwig Studio's library "Presets" folder, which can be found at:

- **Linux and macOS**: "~/Documents/Bitwig Studio/Library/Presets"
- **Windows**: "%userprofile%\Documents\Bitwig Studio\Library\Presets"

> [!NOTE]
> Before installing, ensure you have the full version of **Bitwig Studio**, and it's recommended to use the latest version. This device was specifically tested with **Bitwig Studio version 5.2.5**.

## Usage Guide

### Balance Meter

The **Balance Meter** indicates the perceived center position (balance) within the stereo field. The indicator moves dynamically from left to right, showing whether the left or right channel is more dominant.

> [!TIP]
> For stereo buses, to maintain a well-balanced mix, the indicator should ideally remain in the center.

### Correlation Meter

The **Correlation Meter** displays how well the left and right channels are aligned (phase correlation). The indicator moves dynamically from left (channels are fully out of phase) to right (channels are perfectly in phase).

> [!TIP]
> To aim for good mono compatibility, ensure the indicator remains mostly between the **Center** and the **Right Side**.

### Stereoize Knob

The **Stereoize Knob** adds extra stereo content to a mono or stereo signal (stereo enhancement), with settings ranging from 0% (no effect, default) to 100% (maximum enhancement). Since the **Stereoize Knob** is mono compatible, it won’t produce any audible effect if the **Width Knob** is set to -100% (mono).

> [!TIP]
> Fine-tune the **Stereoize Knob** amount while aiming for a natural-sounding result, then adjust the **Width Knob** amount for desired width. For widening a mono sound, a setting worth trying is **Stereoize** at +67% and **Width** at +57%.

### Width Knob

The **Width Knob** adjusts the width of a stereo signal (side loudness), ranging from -100% (fully mono) to +100% (triple the original width), with a default setting of 0% (unaltered). To widen a mono signal, which lacks side information by definition, use the dedicated **Stereoize Knob**.

> [!TIP]
> To improve coherency in the stereo image, try reducing the width of wider sounds and panning them to distinct positions in the stereo field.

### Panning Knob

The **Panning Knob** shifts the signal's position within the stereo field (true stereo panning), ranging from -100% (hard left) to +100% (hard right), with a default value of 0% (unaltered).

> [!TIP]
> After setting the desired stereo position, experiment with the **Width Knob** amount to improve the overall balance of your mix.

### Meters Knob

The **Meters Knob** adjusts the responsiveness of the meters' movement (average measurement time), ranging from -100% (very slow) to +100% (very fast), with a default value of 0% (balanced).

> [!TIP]
> It's best to stick with a consistent **Meters Knob** setting to build familiarity with the meters' readouts, unless you have a specific need. The default setting is a good starting point.

## Geeky Insights

Ever wondered what's really going on behind the scenes? This section dives deeper for those curious about the inner workings.

**JP Stereo Tool** is a native Bitwig Studio device, using a bit of audio routing trickery to avoid signal alterations introduced by the FX Grid. The meters are visualized through a creative (mis)use of the Steps modulators. CPU usage is generally low but increases slightly when the **Stereoize Knob** is set to a non-zero value. The device adds 34 samples (about 0.7 ms) of compensated latency.

The signal chain within **JP Stereo Tool** follows this order: **Stereoize** > **Width** > **Panning** > **Meters**. This arrangement allows each control to progressively shape the stereo image, with the order of the user interface knobs reflecting the internal signal chain.

If the **Stereoize**, **Width**, or **Panning** knob is moved away from its default position, the device begins shaping the stereo image. When those knobs are set to their default positions, the audio signal is not altered in any way, which is crucial for monitoring-only purposes.

The **Balance Meter** calculates the difference between the RMS (Root Mean Square) values of the left and right channels, normalized by their sum. The **Correlation Meter** calculates the mean product of the left and right channels, normalized by the square root of the product of their RMS values. The **Meters Knob** controls the averaging window time used in the above calculations.

The **Stereoize Knob** splits the signal into three bands using 18 dB per octave crossover filters, and in the middle band applies a comb filtering effect to the left and right channels complementarily. As the amount is raised, the mix between the original and the artificially enhanced signal increases, while the frequency of complementary notches and peaks shifts gradually, making it easier to achieve the optimal sound.

The **Width Knob** is mapped directly to Bitwig Studio's Tool device's Width knob. It works simply by altering the volume of the side signal.

The **Panning Knob** uses true stereo panning, allowing the image to shift without altering the left-right gain relationship. In contrast, typical balance-based panning simply lowers the level of one channel, which can cause parts of a stereo signal to disappear. For example, hard-panning a sound with a ping-pong delay using balance-based panning would make one side inaudible (either "ping" or "pong").

> [!TIP]
> When in doubt, listen to your stereo mix in mono. Believe the meters, but trust your ears, always. May the balance be with you!

## License

You are free to use, modify, and distribute this device in any way you choose. While no attribution is required, feel free to link back to the [GitHub repository](https://github.com/JanuszPelc/StereoTool) if you’d like to credit the project.

For legal details, refer to the full terms provided in the [LICENSE](https://github.com/JanuszPelc/StereoTool/blob/main/LICENSE) file included in the repository.

> [!NOTE]
> This is a hobby project shared as-is. I'll truly appreciate your effort in providing feedback via [Discussions](https://github.com/JanuszPelc/StereoTool/discussions) and submitting [Issues](https://github.com/JanuszPelc/StereoTool/issues), but please be aware that my direct replies may be limited.
