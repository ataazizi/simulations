import numpy as np
import matplotlib.pyplot as plt
from matplotlib.widgets import Button
from mpl_toolkits.mplot3d import Axes3D

# Constants
c = 2.0  # Adjust as needed
a = 5.0  # Adjust as needed

# Define n over a suitable range
n_min = c  # Since arccosh is defined for n/c >= 1
n_max = 5 * c
n_points = 200
n = np.linspace(n_min, n_max, n_points)

# Compute y(n)
y = c * np.arccosh(n / c) + a

# Define y over a suitable range for n(y)
y_min = c * np.arccosh(n_min / c) + a
y_max = c * np.arccosh(n_max / c) + a
y_points = 200
y_vals = np.linspace(y_min, y_max, y_points)

# Compute n(y)
n_inv = c * np.cosh((y_vals - a) / c)

# Create a figure and axes
fig = plt.figure(figsize=(10, 8))
ax = fig.add_subplot(111)
plt.subplots_adjust(bottom=0.25)

# Plot y(n)
line1, = ax.plot(n, y, label=r'$y(n) = c \cdot \cosh^{-1}\left(\frac{n}{c}\right) + a$')

# Plot n(y)
line2, = ax.plot(n_inv, y_vals, label=r'$n(y) = c \cdot \cosh\left(\frac{y - a}{c}\right)$')

ax.set_xlabel('n')
ax.set_ylabel('y')
ax.set_title('2D Plots of y(n) and n(y)')
ax.legend()
ax.grid(True)

# Create a 3D plot but keep it hidden initially
ax3d = fig.add_subplot(111, projection='3d')
ax3d.set_visible(False)

# Compute the 3D surface data for rotation around x-axis
theta_points = 100
theta = np.linspace(0, 2 * np.pi, theta_points)
n_grid, theta_grid = np.meshgrid(n, theta)
y_grid = c * np.arccosh(n_grid / c) + a

# Surface rotated around x-axis
X_x = n_grid
Y_x = y_grid * np.cos(theta_grid)
Z_x = y_grid * np.sin(theta_grid)

# Surface rotated around y-axis
X_y = n_grid * np.cos(theta_grid)
Y_y = y_grid
Z_y = n_grid * np.sin(theta_grid)

# Variables to track the state
is_3d = False
rotation_axis = 'x'  # 'x' or 'y'

# Function to toggle between 2D and 3D plots
def toggle_plot(event):
    global is_3d
    is_3d = not is_3d
    if is_3d:
        # Hide 2D plot and show 3D plot
        ax.set_visible(False)
        ax3d.set_visible(True)
        update_3d_plot()
    else:
        # Hide 3D plot and show 2D plot
        ax3d.set_visible(False)
        ax.set_visible(True)
    plt.draw()

# Function to update the 3D plot based on the rotation axis
def update_3d_plot():
    ax3d.clear()
    if rotation_axis == 'x':
        # Plot surface rotated around x-axis
        ax3d.plot_surface(X_x, Y_x, Z_x, cmap='viridis', edgecolor='none')
        ax3d.set_xlabel('n')
        ax3d.set_ylabel('Y')
        ax3d.set_zlabel('Z')
        ax3d.set_title('3D Surface of Revolution around the x-axis')
    elif rotation_axis == 'y':
        # Plot surface rotated around y-axis
        ax3d.plot_surface(X_y, Y_y, Z_y, cmap='plasma', edgecolor='none')
        ax3d.set_xlabel('X')
        ax3d.set_ylabel('y')
        ax3d.set_zlabel('Z')
        ax3d.set_title('3D Surface of Revolution around the y-axis')
    ax3d.grid(True)

# Function to switch the rotation axis
def switch_axis(event):
    global rotation_axis
    if rotation_axis == 'x':
        rotation_axis = 'y'
    else:
        rotation_axis = 'x'
    if is_3d:
        update_3d_plot()
        plt.draw()

# Add a button to toggle between 2D and 3D plots
ax_button_3d = plt.axes([0.7, 0.1, 0.1, 0.075])
button_3d = Button(ax_button_3d, 'Toggle 3D')
button_3d.on_clicked(toggle_plot)

# Add a button to switch rotation axis
ax_button_axis = plt.axes([0.81, 0.1, 0.1, 0.075])
button_axis = Button(ax_button_axis, 'Switch Axis')
button_axis.on_clicked(switch_axis)

plt.show()
