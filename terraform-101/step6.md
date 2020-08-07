[Variables](https://www.terraform.io/docs/configuration/variables.html) allow
values to be reused throughout your configuration without duplication. Add a
new variable called `foo` to `main.tf`:

<pre class="file" data-filename="main.tf">
variable "foo" {
  description = "a variable for our template"
  default = "SM"
}
</pre>

Now change the variable passed to the `example` template from

```
foo = "SM"
```

to

```
foo = var.foo
```

Now run a `plan`:

```
terraform plan
```{{execute}}

You should see output including is line:

```
No changes. Infrastructure is up-to-date.
```

Now change the `foo` variable from

```
default = "SM"
```

to

```
default = "AYALA"
```

Now run a `plan` again:

```
terraform plan
```{{execute}}

This time you should see some changes:

```
  - SM is a leading Philippine company that is invested in market leading businesses in retail, banking and property.
  + AYALA is a leading Philippine company that is invested in market leading businesses in retail, banking and property.
```

Apply the changes:

```
terraform apply
```{{execute}}

Again, type `yes` when prompted.

View the contents of the file with the `cat` command:

```
cat example.txt
```{{execute}}
