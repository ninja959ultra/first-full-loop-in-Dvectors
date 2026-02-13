# first-full-loop-in-Dvectors

This code will excute a plot with a point (bot) that try to achieve to the target

I've used:
- Dot Product
- Cross Product
- Magintude using math.sqrt()

```
import math
import matplotlib.pyplot as plt

# Based Information
current_point = (-7,-4)
bot_direction = (1,0)
target_point = (25,25)
speed = 2 # m/s
delta_time = 0.5 # Seconds
turn_rate = 0.1


# For plot
plt.ion()
fig, ax = plt.subplots()
ax.set_xlim(-30, 30)
ax.set_ylim(-30, 30)
ax.set_aspect('equal')
bot, = ax.plot([current_point[0]], [current_point[1]], marker='o', color='red')


while True:
    sub_point = (target_point[0]-current_point[0], target_point[1]-current_point[1])
    magintude = math.sqrt(sub_point[0]**2 + sub_point[1]**2)

    if magintude < 2:
        print('The bot on the target')
        break

    target_direction = (sub_point[0]/magintude, sub_point[1]/magintude)

    DPresult = bot_direction[0]*target_direction[0] + bot_direction[1]*target_direction[1]
    CPresult = bot_direction[0]*target_direction[1] - bot_direction[1]*target_direction[0]

    if CPresult == 0 and DPresult == 1: # If the bot is directly the same direction of target
        sx = target_direction[0]*speed
        sy = target_direction[1]*speed

        new_point = (current_point[0]+sx, current_point[1]+sy)

        current_point = new_point

    if DPresult > 0: # If the bot close to the target direction
        if CPresult > 0: # Move and turn Left
            print('Turn Left')

            theta = math.radians(15) # Degree is positve becausewe turn left
            new_dx = bot_direction[0]*math.cos(theta)-bot_direction[1]*math.sin(theta)
            new_dy = bot_direction[0]*math.sin(theta)+bot_direction[1]*math.cos(theta)
            new_bot_direction = (new_dx, new_dy)

            sx = target_direction[0]*speed
            sy = target_direction[1]*speed
            new_point = (current_point[0]+sx, current_point[1]+sy)

            current_point = new_point
            bot_direction = new_bot_direction


        elif CPresult < 0: # Move and turn Right
            print('Turn Right')

            theta = math.radians(-15) # Degree is Negative becausewe turn Right
            new_dx = bot_direction[0]*math.cos(theta)-bot_direction[1]*math.sin(theta)
            new_dy = bot_direction[0]*math.sin(theta)+bot_direction[1]*math.cos(theta)
            new_bot_direction = (new_dx, new_dy)

            sx = target_direction[0]*speed
            sy = target_direction[1]*speed
            new_point = (current_point[0]+sx, current_point[1]+sy)

            current_point = new_point
            bot_direction = new_bot_direction


    
    else: # Stay where you are and turn
        print('Turn without moving')

        if CPresult > 0: # Turn Left
            print('Turn Left')

            theta = math.radians(15) # Degree is positve because we turn left
            new_dx = bot_direction[0]*math.cos(theta)-bot_direction[1]*math.sin(theta)
            new_dy = bot_direction[0]*math.sin(theta)+bot_direction[1]*math.cos(theta)
            new_bot_direction = (new_dx, new_dy)   

            bot_direction = new_bot_direction         

        elif CPresult < 0:
            print('Turn Right')

            theta = math.radians(-15) # Degree is Negative because we turn Right
            new_dx = bot_direction[0]*math.cos(theta)-bot_direction[1]*math.sin(theta)
            new_dy = bot_direction[0]*math.sin(theta)+bot_direction[1]*math.cos(theta)
            new_bot_direction = (new_dx, new_dy)

            bot_direction = new_bot_direction

        else: # Oppsite              
            theta = math.radians(180) # Degree is Negative because we turn Right
            new_dx = bot_direction[0]*math.cos(theta)-bot_direction[1]*math.sin(theta)
            new_dy = bot_direction[0]*math.sin(theta)+bot_direction[1]*math.cos(theta)
            new_bot_direction = (new_dx, new_dy)

            bot_direction = new_bot_direction

    bot.set_data([current_point[0]], [current_point[1]])
    ax.quiver(current_point[0], current_point[1], bot_direction[0], bot_direction[1], color='blue', scale=5)
    plt.pause(delta_time)

plt.ioff()
plt.show()
```
