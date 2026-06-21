# 6-DOF Robot Manipulator Simulation (OpenGL)

A real-time 3D simulation and visualization of a 6-DOF robot arm, written in C
with OpenGL/GLUT. It computes the arm's kinematics, draws it on an interactive
grid, follows point-to-point trajectories, and can stream joint commands to a
physical robot over a serial port.

Originally built as a robotics course project at the Department of Electrical
Engineering, **Universitas Indonesia** (2022).

## Demo

<video src="https://github.com/hanifedma/robot-6dof-opengl/raw/master/demo.mp4"
       poster="https://github.com/hanifedma/robot-6dof-opengl/raw/master/poster.jpg"
       autoplay loop muted playsinline controls width="640"></video>

> If the player above doesn't load, watch it here: [demo.mp4](https://github.com/hanifedma/robot-6dof-opengl/raw/master/demo.mp4)

## Features

- **Forward kinematics** — computes the end-effector pose from the six joint
  angles (`forward_kinematic()` in `planargl.c`).
- **Inverse kinematics** — Jacobian pseudoinverse (`J^T (J J^T)^{-1}`) to drive
  the end-effector toward a commanded Cartesian position (`inverse_jacobian()`).
- **Trajectory generation** — linear point-to-point interpolation between the
  current and commanded pose (`trajectory_line()`).
- **3D visualization** — OpenGL/GLUT rendering of the links, joints, and a
  reference floor grid, with an adjustable camera.
- **Serial communication** — optional link to a physical robot (`serial.h`).

## Build

Requires a C/C++ compiler and the OpenGL + GLUT development libraries.

On Debian/Ubuntu:

```bash
sudo apt install build-essential freeglut3-dev libglu1-mesa-dev
make
```

This produces the `planar` binary.

## Run

```bash
./planar
```

### Controls

| Key | Action |
| --- | --- |
| `1`–`6` | Increase joint angle q1–q6 |
| `!` `@` `#` `$` `%` `^` | Decrease joint angle q1–q6 (Shift + 1–6) |
| `m` | Toggle manual mode |
| `u`/`U`, `i`/`I`, `o`/`O` | Translate the camera (±x, ±y, ±z) |
| `j`/`J`, `k`/`K`, `l`/`L` | Rotate the camera about x, y, z |
| `Esc` | Quit |

> The serial link defaults to `/dev/com2` (Windows) / `/dev/ttyS0` (Linux) in
> `serial.h`; adjust the port there for your setup, or run the simulation
> without a connected robot.

## Acknowledgements

The OpenGL template was provided for the robotics course by
**Dr. Abdul Muis, M.Eng.**, Autonomous Control & Electronics (ACONICS)
Research Group, Department of Electrical Engineering, Universitas Indonesia.

## Author

Hanif Edma Fauz
