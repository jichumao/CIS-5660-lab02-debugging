# lab02-debugging

# Showcase
[Link to Shadertoy]()
Img Here
# 4 Bugs
```

void raycast() {
    ...
    V *= len;
    // bug here 1/5 should use correct formula
    //H *= len * iResolution.x / iResolution.x;
    H *= len * iResolution.x / iResolution.y;
    ..
}

void march() {
    t = 0.001;
    // bug here 2/5 we need to increase the iterations to get more hit points
    //for(int i = 0; i < 64; ++i) {
    for(int i = 0; i < 128; ++i) {
}

Intersection sdf3D(vec3 dir, vec3 eye) {
    ...
    // bug here
    // dir = reflect(eye, nor); 3/5
    dir = reflect(dir, nor);
    march(isect + dir * 0.01, dir, t, hitObj);
   ...
}

void mainImage( out vec4 fragColor, in vec2 fragCoord ) {
    // Normalized pixel coordinates (from 0 to 1)
    vec2 uv = fragCoord/iResolution.xy;
    // [-1, 1]
    // Variable should not be declared again, bug 4/5
    uv = 2.0 * uv - vec2(1.0);

```
# Setup 

Create a [Shadertoy account](https://www.shadertoy.com/). Either fork this shadertoy, or create a new shadertoy and copy the code from the [Debugging Puzzle](https://www.shadertoy.com/view/flGfRc).

Let's practice debugging! We have a broken shader. It should produce output that looks like this:
[Unbelievably beautiful shader](https://user-images.githubusercontent.com/1758825/200729570-8e10a37a-345d-4aff-8eff-6baf54a32a40.webm)

It don't do that. Correct THREE of the FIVE bugs that are messing up the output. You are STRONGLY ENCOURAGED to work with a partner and pair program to force you to talk about your debugging thought process out loud.

Extra credit if you can find all FIVE bugs.

# Submission
- Create a pull request to this repository
- In the README, include the names of both your team members
- In the README, create a link to your shader toy solution with the bugs corrected
- In the README, describe each bug you found and include a sentence about HOW you found it.
- Make sure all three of your shadertoys are set to UNLISTED or PUBLIC (so we can see them!)
