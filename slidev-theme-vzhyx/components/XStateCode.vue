<template>
	<CodePhone :code="code" />
</template>

<script setup>
const code = `import { createMachine, assign } from 'xstate';

const trafficLightMachine = createMachine({
  id: 'trafficLight',
  initial: 'red',
  context: {
    prevState: null
  },
  states: {
    red: {
      exit: assign({ prevState: 'red' }),
      on: {
        NEXT: 'yellow'
      }
    },
    yellow: {
      on: {
        NEXT: [
          {
            target: 'green',
            guard: (context) => context.prevState === 'red'
          },
          {
            target: 'red',
            guard: (context) => context.prevState === 'green'
          }
        ]
      }
    },
    green: {
      exit: assign({ prevState: 'green' }),
      on: {
        NEXT: 'yellow'
      }
    }
  }
});

// Цикл: red -> yellow -> green -> yellow -> red -> ...

const [state, send] = useMachine(trafficLightMachine);
send('NEXT');`;
</script>

