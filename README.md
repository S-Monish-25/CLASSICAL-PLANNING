# ExpNo:10 Implementation of Classical Planning Algorithm
# Algorithm or Steps Involved:
<ol>
  <li>Define the initial state</li>
  <li>Define the goal state</li>
  <li>Define the actions</li>
  <li>Find a <b>plan</b> to reach the goal state</li>
  <li>Print the plan</li>
</ol>

# Example - 1
```
initial_state = {'A': 'Table', 'B': 'Table'}
goal_state = {'A': 'B', 'B': 'Table'}

actions = {
    'move_A_to_B': {'precondition': {'A': 'Table', 'B': 'Table'}, 'effect': {'A': 'B'}},
    'move_B_to_Table': {'precondition': {'A': 'Table', 'B': 'B'}, 'effect': {'B': 'Table'}}
}

plan = find_plan(initial_state, goal_state, actions)
print(plan)
```
# Output:
```
['move_A_to_B']
```
# Example - 2
```
initial_state = {'A': 'Table', 'B': 'Table', 'C': 'Table'}
goal_state = {'A': 'B', 'B': 'C', 'C': 'Table'}

actions = {
    'move_A_to_B': {'precondition': {'A': 'Table', 'B': 'Table'}, 'effect': {'A': 'B'}},
    'move_B_to_C': {'precondition': {'A': 'B', 'B': 'Table', 'C': 'Table'}, 'effect': {'B': 'C'}},
    'move_C_to_Table': {'precondition': {'A': 'B', 'B': 'C', 'C': 'C'}, 'effect': {'C': 'Table'}}
}

plan = find_plan(initial_state, goal_state, actions)
print(plan)
```
# Output:
```
['move_A_to_B', 'move_B_to_C']
```
## PROGRAM:
~~~
from collections import deque

# Check whether the current state is the goal state
def is_goal(current_state, goal_state):
    return current_state == goal_state

# Check if an action can be applied
def applicable(current_state, action):
    for key, value in action["precondition"].items():
        if current_state.get(key) != value:
            return False
    return True

# Apply an action and return the new state
def apply_action(current_state, action):
    new_state = current_state.copy()
    new_state.update(action["effect"])
    return new_state

# Find a plan using Breadth-First Search (BFS)
def find_plan(initial_state, goal_state, actions):
    queue = deque()
    queue.append((initial_state, []))
    visited = set()

    while queue:
        current_state, plan = queue.popleft()

        # Convert dictionary to hashable form
        state_key = tuple(sorted(current_state.items()))

        if state_key in visited:
            continue
        visited.add(state_key)

        # Goal Test
        if is_goal(current_state, goal_state):
            return plan

        # Try every action
        for action_name, action in actions.items():
            if applicable(current_state, action):
                new_state = apply_action(current_state, action)
                queue.append((new_state, plan + [action_name]))

    return None


# -------------------------
# Example 1
# -------------------------

print("Example 1")

initial_state = {
    'A': 'Table',
    'B': 'Table'
}

goal_state = {
    'A': 'B',
    'B': 'Table'
}

actions = {
    'move_A_to_B': {
        'precondition': {
            'A': 'Table',
            'B': 'Table'
        },
        'effect': {
            'A': 'B'
        }
    },

    'move_B_to_Table': {
        'precondition': {
            'A': 'Table',
            'B': 'B'
        },
        'effect': {
            'B': 'Table'
        }
    }
}

plan = find_plan(initial_state, goal_state, actions)
print("Plan:", plan)


# -------------------------
# Example 2
# -------------------------

print("\nExample 2")

initial_state = {
    'A': 'Table',
    'B': 'Table',
    'C': 'Table'
}

goal_state = {
    'A': 'B',
    'B': 'C',
    'C': 'Table'
}

actions = {
    'move_A_to_B': {
        'precondition': {
            'A': 'Table',
            'B': 'Table'
        },
        'effect': {
            'A': 'B'
        }
    },

    'move_B_to_C': {
        'precondition': {
            'A': 'B',
            'B': 'Table',
            'C': 'Table'
        },
        'effect': {
            'B': 'C'
        }
    },

    'move_C_to_Table': {
        'precondition': {
            'A': 'B',
            'B': 'C',
            'C': 'C'
        },
        'effect': {
            'C': 'Table'
        }
    }
}

plan = find_plan(initial_state, goal_state, actions)
print("Plan:", plan)
~~~

## OUTPUT:

<img width="631" height="240" alt="image" src="https://github.com/user-attachments/assets/7cb29abb-d50f-4364-834b-2b1d9df4d5e8" />



## RESULT:

Thus the program is executed successfully.
