# LearnCI

this file use to test Circle CI

# test
Webhook

# EX1: Attach resource from diffence job
version: 2.1

jobs:
  save_hello_world:
    docker:
      - image: cimg/base:2023.03
    steps:
      - run: echo "hello world" > ~/output.txt
      - persist_to_workspace:
          root: ~/
          paths:
            - output.txt
  print_hello_world:
    docker:
      - image: cimg/base:2023.03
    steps:
      - attach_workspace:
          at: ~/
      - run: cat ~/output.txt

# Orchestrate our job run sequence
workflows:
  build_and_test:
    jobs:
      - save_hello_world
      - print_hello_world:
          requires:
            - save_hello_world
