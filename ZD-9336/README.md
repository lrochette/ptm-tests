# Issue

128  error     "steps" must be an object  
128  error     "true" is not allowed
128  error     "true" is not allowed
165  error     "steps" must be an object
165  error     "true" is not allowed

## test1
on is betwee quote to prevent conversion into a boolean

## test2
on is as-is to see if awk usage to put it between quote works

# debuggging

looks like `yq` interpreted on: as true

segment of my codefresh-spec.yaml that looks like:

```
      when:
        steps:
        - name: call_deploy_test_pipeline
          on:
            - success
        - name: integration_tests
          on:
            - success    
```

the output from yq from combining the spec + triggers looks like:

```
      when:
        steps:
          - name: call_deploy_test_pipeline
            'true':
              - success
          - name: integration_tests
            'true':
              - success
```
