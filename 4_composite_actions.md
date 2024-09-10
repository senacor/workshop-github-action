# Composite actions - Building (and publishing) custom actions 

## Extract logic from multiple actions

There are often steps which need to be repeated with different inputs. 
These steps can be extracted and reused, just like in software development the dry principle.

### Composite action
``.github/actions/extracted-step/action.yaml``
```yaml
name: Greet and create
description: 'Greet someone and create a random number as output'
inputs:
  who-to-greet: 
    description: 'Who to greet'
    required: true
outputs:
  random-number:
    description: "Random generated number"
    value: ${{ steps.random-number-generator.outputs.random-number }}
runs:
  using: "composite"
  steps:
    - name: Set Greeting
      run: echo "Hello $INPUT_WHO_TO_GREET."
      shell: bash
      env:
        INPUT_WHO_TO_GREET: ${{ inputs.who-to-greet }}
    - name: Random Number Generator
      id: random-number-generator
      run: echo "random-number=$(echo $RANDOM)" >> $GITHUB_OUTPUT
      shell: bash
```

### Using composite action
``.github/workflows/example.yaml``
```yaml
jobs:
  greet-randomize:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - id: greet-and-randomize
        uses: ./.github/actions/greet-and-randomize
        with:
          who-to-greet: 'Hack&Heat'
      - run: echo random-number "$RANDOM_NUMBER"
        shell: bash
        env:
          RANDOM_NUMBER: ${{ steps.greet-and-randomize.outputs.random-number }}
```

## Creating complex actions

-> https://github.com/senacor/workshop-github-action-action

### Integration

```yaml
  greet-randomize-external:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - id: greet-and-randomize
        uses: senacor/workshop-github-action-action@v1.0.1
        with:
          who-to-greet: 'Hack&Heat'
      - run: echo random-number "$RANDOM_NUMBER"
        shell: bash
        env:
          RANDOM_NUMBER: ${{ steps.greet-and-randomize.outputs.random-number }}
```