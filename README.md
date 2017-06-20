# Pass args and env vars to a task in the Gradle new software model


This is a demo of how to pass arguments and environment variables from a
`BinarySpec` to a custom task.

## Arguments

Passing args to custom tasks is relatively easy, and the
best practice is shown in [Idiomatic Gradle Plugin (slide
15)](http://www.slideshare.net/ysb33r/idiomatic-ggradle-plugin-writing).

Passing args from the new model DSL to the custom task is shown in the 
`build.gradle` file in this repository.

From the user point of view, setting arguments in the DSL looks like this:

```
model {
    components {
        juiceComponent(JuiceComponent) {
            binaries {
                apple(JuiceBinarySpec) {
                    args = ['empire', 'melba']
                    args += ['mcintosh']
               }
            }
            ....
        }
    }
}
```

## Environment variables

Environment variables can be represented as a map of strings: `Map<String, String>`.
The new software model supports a construct called a `ModelMap`, e.g. `ModelMap<T>`.

Passing a `Map` to a custom task is described
in [Idiomatic Gradle Plugin Writing (slides
16-18)](http://www.slideshare.net/ysb33r/idiomatic-ggradle-plugin-writing),
but passing a `Map` via the new model DSL is not as easy.


The best I could looks like this:

```
model {
    components {
        juiceComponent(JuiceComponent) {
            binaries {
                // Describe the distributions
                apple(JuiceBinarySpec) {
                    envVars {
                        var1(EnvVar) { value = 'value1'}
                        var2(EnvVar) { value = 'value2'}
                    }
                }
            }
            ...
        }
    }
}
```

