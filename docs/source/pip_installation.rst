Installation
============


Installing Isaac Sim
--------------------

.. note::

   The installation of Isaac Sim is in `official documentation. <https://docs.omniverse.nvidia.com/isaacsim/latest/installation/index.html>`_
   please refer to it.

Installing Isaac Lab
--------------------

Cloning Isaac Lab
~~~~~~~~~~~~~~~~~

.. note::

   In this document, we use `forked repository <https://github.com/IROL-SSU/IsaacLab/>`_ of Isaac Lab for code management used in R&D.
   

Clone the Isaac Lab repository in the workspace:

.. tab-set::

   .. tab-item:: HTTPS

      .. code:: bash

         git clone https://github.com/IROL-SSU/IsaacLab.git


-  Install dependencies using ``apt`` (on Ubuntu):

.. code:: bash

   sudo apt install cmake build-essential

.. tab-set::
   :sync-group: os

   .. tab-item:: Linux
      :sync: linux

      .. code:: bash

         ./isaaclab.sh --install # or "./isaaclab.sh -i"


Testing Reinforcement Learning Environment
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. note::

   Run the examples below to verify that the training through each reinforcement learning library is running normally.

We provide wrappers to different reinforcement libraries. These wrappers convert the data from the environments
into the respective libraries function argument and return types.

-  Training an agent with
   `Stable-Baselines3 <https://stable-baselines3.readthedocs.io/en/master/index.html>`__
   on ``Isaac-Cartpole-v0``:

   .. code:: bash

      # install python module (for stable-baselines3)
      ./isaaclab.sh -i sb3
      # run script for training
      # note: we enable cpu flag since SB3 doesn't optimize for GPU anyway
      ./isaaclab.sh -p source/standalone/workflows/sb3/train.py --task Isaac-Cartpole-v0 --headless --cpu
      # run script for playing with 32 environments
      ./isaaclab.sh -p source/standalone/workflows/sb3/play.py --task Isaac-Cartpole-v0 --num_envs 32 --checkpoint /PATH/TO/model.zip

-  Training an agent with
   `SKRL <https://skrl.readthedocs.io>`__ on ``Isaac-Reach-Franka-v0``:

   .. code:: bash

      # install python module (for skrl)
      ./isaaclab.sh -i skrl
      # run script for training
      ./isaaclab.sh -p source/standalone/workflows/skrl/train.py --task Isaac-Reach-Franka-v0 --headless
      # run script for playing with 32 environments
      ./isaaclab.sh -p source/standalone/workflows/skrl/play.py --task Isaac-Reach-Franka-v0 --num_envs 32 --checkpoint /PATH/TO/model.pt

-  Training an agent with
   `RL-Games <https://github.com/Denys88/rl_games>`__ on ``Isaac-Ant-v0``:

   .. code:: bash

      # install python module (for rl-games)
      ./isaaclab.sh -i rl_games
      # run script for training
      ./isaaclab.sh -p source/standalone/workflows/rl_games/train.py --task Isaac-Ant-v0 --headless
      # run script for playing with 32 environments
      ./isaaclab.sh -p source/standalone/workflows/rl_games/play.py --task Isaac-Ant-v0 --num_envs 32 --checkpoint /PATH/TO/model.pth

-  Training an agent with
   `RSL-RL <https://github.com/leggedrobotics/rsl_rl>`__ on ``Isaac-Reach-Franka-v0``:

   .. code:: bash

      # install python module (for rsl-rl)
      ./isaaclab.sh -i rsl_rl
      # run script for training
      ./isaaclab.sh -p source/standalone/workflows/rsl_rl/train.py --task Isaac-Reach-Franka-v0 --headless
      # run script for playing with 32 environments
      ./isaaclab.sh -p source/standalone/workflows/rsl_rl/play.py --task Isaac-Reach-Franka-v0 --num_envs 32 --load_run run_folder_name --checkpoint model.pt

All the scripts above log the training progress to `Tensorboard`_ in the ``logs`` directory in the root of
the repository. The logs directory follows the pattern ``logs/<library>/<task>/<date-time>``, where ``<library>``
is the name of the learning framework, ``<task>`` is the task name, and ``<date-time>`` is the timestamp at
which the training script was executed.

To view the logs, run:

.. code:: bash

   # execute from the root directory of the repository
   ./isaaclab.sh -p -m tensorboard.main --logdir=logs

.. _Tensorboard: https://www.tensorflow.org/tensorboard