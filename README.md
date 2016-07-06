# Reading args from a binary spec is not possible unless set in the DSL model

This is a twist on the master branch version of this demo.

In this example, we prove that it is not possible to read the binary spec `args`
property, unless that property is set in the DSL model. It is important to be able
to read this property so it can be copied to the task.

To see the problem, simply clone this branch of the repo and run it with Gradle 2.13:

```
$ gradle Juicer
...
 > Cannot set value for model element 'components.juiceComponent.binaries.orange.args' as this element is not mutable.
```

The relevant snippets of code are the task mutator, and the model DSL:

```
@BinaryTasks
void generateTasks(ModelMap<Task> tasks, final JuiceBinarySpec binary) {
    tasks.create("Juicer", DefaultTask) { task ->
        // Next line throws exception, unless the value is set in the model
        println(binary.args)
    }
}
...
model {
    components {
        juiceComponent(JuiceComponent) {
            binaries {
                orange(JuiceBinarySpec) {
                    // Uncomment out the next line to make the exception go away
                    //args = ['a']
                }
            }
        }
    }
}
```

The full code is in `build.gradle`.
