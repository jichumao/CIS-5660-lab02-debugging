# lab02-debugging
* Jichu Mao
  * [LinkedIn](https://www.linkedin.com/in/jichu-mao-a3a980226/)
  *  [Personal Website](https://jichu.art/)
    
# Showcase

[Link to Shadertoy](https://www.shadertoy.com/view/lXfcD2)
![](lab2.gif)

# Bugs
Successfully identified and fixed all bugs！

```
void raycast(vec2 uv, out vec3 dir,
             out vec3 eye, out vec3 ref) {
...
    vec3 H = normalize(cross(vec3(0.0, 1.0, 0.0), ref - eye));
    vec3 V = normalize(cross(H, eye - ref));
    V *= len;
// bug here, should use correct formula
    //H *= len * iResolution.x / iResolution.x;
    H *= len * iResolution.x / iResolution.y;
    vec3 p = ref + uv.x * H + uv.y * V;
    dir = normalize(p - eye);
}

void march(vec3 origin, vec3 dir, out float t, out int hitObj) {
    t = 0.001;
// bug here  we need to increase the iterations to get more hit points
    //for(int i = 0; i < 64; ++i) {
    for(int i = 0; i < 128; ++i) {
        vec3 pos = origin + t * dir;
    	float m;
        sceneMap3D(pos, m, hitObj);
        if(m < 0.01) {
            return;
        }
        t += m;
    }
    t = -1.0;
    hitObj = -1;
}

Intersection sdf3D(vec3 dir, vec3 eye) {
// use hitObj == -1 instead of t == -1
    if (hitObj == -1){
    //if(t == -1.0) {  
        return Intersection(t, skyColor(dir), vec3(eye + 1000.0 * dir), -1);
    }

    vec3 isect = eye + t * dir;
    vec3 nor = computeNormal(isect);
    
    vec3 material = computeMaterial(hitObj, isect, dir, nor);
    // bug here
    // dir = reflect(eye, nor); 
    dir = reflect(dir, nor);
...
}

// Bug here : Compiler Error,bariable should not be declared again
void mainImage( ) {
    // Normalized pixel coordinates (from 0 to 1)
    vec2 uv = fragCoord/iResolution.xy;
    // [-1, 1]
    // Variable should not be declared again, bug here
    uv = 2.0 * uv - vec2(1.0);
}
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
