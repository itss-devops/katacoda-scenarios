The template provider can be used to generate files that can be passed to
many types of resources.

Let's experiement with a simple one-line template. Add the configuration
below to `main.tf`:

<pre class="file" data-filename="main.tf">
data "template_file" "example" {
  vars = {
    foo = "SM"
  }

  template = "$${foo} is a leading Philippine company that is invested in market leading businesses in retail, banking and property.\n"
}
</pre>

Here we have a `template_file`
[data source](https://www.terraform.io/docs/configuration/data-sources.html)
named `example` which passes a variable `foo` to the template. Note that in
this syntax the `foo` variable must be references with `$$`.

We can write a file `example.txt` to the current directory from this template
with the [local provider](https://www.terraform.io/docs/providers/local/index.html)
using the `local_file`
[resource](https://www.terraform.io/docs/configuration/resources.html). Add
the configuration below to `main.tf`:

<pre class="file" data-filename="main.tf">
resource "local_file" "example" {
  content  = data.template_file.example.rendered
  filename = "example.txt"
}
</pre>

Resources are the most important element in the Terraform language. Each
`resource` block describes one or more managed resources.

Since we have added a resource for a new provider, we must run `init`
again to download it:

```
terraform init
```{{execute}}

You should see output including this line:

```
- Downloading plugin for provider "local" (hashicorp/local) 1.4.0...
```

Hopefully you noticed that we haven't specified a version for the `local`
provider, so Terraform just downloaded the latest version. How could you have
specified a version for the `local` provider?
