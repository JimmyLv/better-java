## Configuration management 配置管理

So now you've got your code compiled, your repository set up, and you need to
get your code out in your development environment and eventually push it to
production. Don't skimp here, because automating this will pay dividends for a
long time.

所以目前为止，你已经编译好代码，设置好仓库，然后你需要将代码从开发环境拿出来，最终部署到产品环境。不要在这里有所吝啬，因为自动化将会节约非常多的时间。

[Chef][chef], [Puppet][puppet], and [Ansible][ansible] are typical choices.
I've written an alternative called [Squadron][squadron], which I, of course,
think you should check out because it's easier to get right than the
alternatives.

[Chef][chef]、[Puppet][puppet]和[Ansible][ansible]都是非常典型的选择。我也写过另外一个叫[Squadron][squadron]的工具，当然，我觉得你可以试试，因为它比其他选择更加容易上手。

Regardless of what tool you choose, don't forget to automate your deployments.

无论你选择什么工具，不要忘记部署自动化。

[chef]: http://www.getchef.com/chef/
[puppet]: http://puppetlabs.com/
[ansible]: http://www.ansible.com/home
[squadron]: http://www.gosquadron.com
