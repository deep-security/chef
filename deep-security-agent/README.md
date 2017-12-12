A collection of recipes to help deploy and manage the Deep Security agent.

## Requirements

All of the recipes in this cookbook require a working Deep Security infrastructure. The key component is the Deep Security manager. The agents (which these recipes help you manage) do the heavy lifting but the manager gives the marching orders. 

There are no specific technical requirements beyond a standard Chef deployment.


## Attributes

#### Recipe : deep-security-agent::default

Key | Type | Description | Default
----|------|-------------|--------
['dsm_agent_download_hostname'] | String | Hostname of the Deep Security manager | app.deepsecurity.trendmicro.com
['dsm_agent_download_port'] | Int | The port to connect to the Deep Security manager on to download the agents. This is typically the same port as the admin web access. | 443
['ignore_ssl_validation'] | Boolean |  Whether or not to ignore the SSL certificate validation for agent downloads. Marketplace and software deployments ship with self-signed certificates and require this set to 'true'. | false
['dsm_agent_activation_hostname'] | String | The hostname for the agents to communicate with once deployed. For Marketplace and software deployments this is typically the same hostname as 'dsm_agent_download_hostname'. | agents.deepsecurity.trendmicro.com
['dsm_agent_activation_port'] | Int | The post to use for the agent heartbeat (the regular communication). For Marketplace and software deployments, the default is 4118. | 443
['tenant_id'] | String | In a multi-tenant installation (like Deep Security as a Service), this identifies the tenant account to register the agent with. | nil
['token'] | String | In a multi-tenant installation (like Deep Security as a Service), this identifies the tenant account to register the agent with. | nil
['policy_id'] | String | The Deep Security ID assigned to the policy to apply to the agents on activation. | nil


## Usage

#### Recipe : deep-security-agent::default

Make sure that you include 'deep-security-agent' in your node's 'run_list'. This will ensure that the Deep Security agent is installed (it's the default.rb recipe).

```json
{
  "name":"my_node",
  "default_attributes": {
    "deep_security_agent" : {
      "dsm_agent_download_hostname": "app.deepsecurity.trendmicro.com",
      "dsm_agent_download_port" : "443",
      "dsm_agent_activation_hostname" : "agents.deepsecurity.trendmicro.com",
      "dsm_agent_activation_port" : "443",
      "tenant_id" : "<Deep Security DSAAS Tenant ID>",
      "token" : "<Deep Security DSAAS Tenant Token>"
	}
  },
  "run_list": [
    "recipe[deep-security-agent::default]"
  ]
}
```