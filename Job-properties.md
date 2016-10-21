# Job Properties

## Development
1. Add a constant for each property in the executor class. See WebSphereMQJobExecutor for an example
2. For each constant create a label in the message catalog
3. Pass the properties as a parameter of the doAction method
4. In the doAction method set the properties
5. In the changeStatus method pass the properties as parameter

## Verification
1. Run the job
2. Check the properties on the TDWC
3. Check the properties on conman (conman sj ...; props)
4. Try to import the exported properties as variables in a subsequent job

## Documentation
1. Document the name and the value of the properties