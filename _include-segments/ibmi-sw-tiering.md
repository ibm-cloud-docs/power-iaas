
[IBMi-virtual-sw-tiering-July-25-start]{: tag-green}

## Virtual software tiers for IBM i


For the IBM i operating system (OS) starting with Power10 servers, virtual software tiers provide a mechanism to limit the size of the LPAR for a particular pricing tier but allow it to run on any class of system. For example, a 1-core virtual machine could be assigned a P10 tier whether it is on an S1022 or an E1080, but that partition cannot grow (i.e., be resized) beyond the “business rules” of that pricing tier.


As a client, I want to be able to view the details of virtual tiers with the
maximum processors and memory for each virtual tier.

As a client, I want to be able to optionally select a virtual tier while deploying
a VM (assigning VSN is a prerequisite for a virtual tier), so that I can optimize
my associated operating system and/or ISV software licensing charges.

As a client, I want to be able to change the virtual tier for a VM, so that I have
flexibility to change tiers as needed.

Note that it’s currently a technical prerequisite that the VM must be powered
off in order to change the virtual tier.

As a client, I want to be able to view the virtual tier associated with a VM, so
that I can understand how my VM and associated software will be charged.

As a client, I want to be able to deploy VMs with different virtual tiers across
different types of systems (e.g., S1022, E1080), so that I have flexibility to
optimize the underlying hardware charges I pay for cores and memory.



[IBMi-virtual-sw-tiering-July-25-end]{: tag-green}
