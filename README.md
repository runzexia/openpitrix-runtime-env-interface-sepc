Public API for RuntimeEnvService :

* CreateRuntimeEnv
* DescribeRuntimeEnvs
* ModifyRuntimeEnv
* DeleteRuntimeEnv
* CreateRuntimeEnvCredential
* DescribeRuntimeEnvCredentials
* ModifyRuntimeEnvCredential
* DeleteRuntimeEnvCredential
* AttachCredentialToRuntimeEnv
* DetachCredentialFromRuntimeEnv


## User create runtime_env 

1. select runtime label qingcloud/kubernetes
2. input endpoint URL
3. validate URL
4. set runtime_env label

## User create runtime_env_credential 

1. select runtime_env
2. input runtime_env_credential 
3. validate credential 

## Runtime Env Manager Interface Spec

* CreateRuntimeEnv

  Request Parameters

  | Parameter name | Type   | Description                                     | Required |
  | -------------- | ------ | ----------------------------------------------- | -------- |
  | name           | String | name of runtime_env                             | Yes      |
  | description    | String | description of runtime_env                      | No       |
  | labels          | String   | labels of runtime_env, "runtime" label is required, vm_based-runtime "zone" is required format "runtime=qingcloud,env=production" | Yes      |
  | runtime_env_url            | String | url of runtime_env                         | Yes      |

  Response Elements

  | Parameter name | Type    | Description                             |
  | -------------- | ------- | --------------------------------------- |
  | action         | String  | the corresponding action                |
  | runtime_env_id | String  | id of runtime_env                       |

* DescribeRuntimeEnvs

  Request Parameters

  | Parameter name | Type   | Description                                              | Required |
  | -------------- | ------ | -------------------------------------------------------- | -------- |
  | search_word    | String | search keyword, support runtime_env name | No       |
  | status         | Array | status of runtime_envs                                  | No       |
  | runtime_env_ids | Array  | id of runtime_envs                                       | No       |
  | selector | String  | selector of runtime_envs,format "runtime=qingcloud,runtime=aws,env=production"| No       |
  | owner         | String  | owner of runtime_envs                                   | No       |
  | limit  | Integer | size of one page, default 10 ,max 100 | No |
  | offset | Integer | data offset, default 0  | No |
  | verbose | Integer | if 1 returns verbose information | No |

  Response Elements

  | Parameter name  | Type    | Description                             |
  | --------------- | ------- | --------------------------------------- |
  | action          | String  | the corresponding action                |
  | runtime_env_set | Array   | JSON format runtime_env array           |
  | total_count     | Integer | count of runtime_env_set                |


  Response Item

  | Parameter name             | Type   | Description                                                  |
  | -------------------------- | ------ | ------------------------------------------------------------ |
  | runtime_env_id             | String | id of runtime_env                                            |
  | name                       | String | name of runtime_env                                          |
  | description                | String | description of runtime_env                                   |
  | runtime_env_url                   | String | url of runtime_env                                      |
  | runtime_env_credential_id | String  | crendential attached to runtime_env, return this value when verbose = 1 |
  | labels         | String  | labels of runtime_env,format "runtime=qingcloud,runtime=aws,env=production"|
  | owner                      | String | owner of runtime_env                                         |
  | status                     | String | status of runtime_env                                        |
  | create_time                | Timestamp | create_time of runtime_env                                        |
  | status_time                     | Timestamp | status_time of runtime_env                                        |


* ModifyRuntimeEnv

  Request Parameters

  | Parameter name | Type   | Description                | Required |
  | -------------- | ------ | -------------------------- | -------- |
  | runtime_env_id | String | id of runtime_env          | Yes      |
  | name           | String | name of runtime_env        | No       |
  | description    | String | description of runtime_env | No       |
  | labels         | String  | runtime_env labels,  overwrite the current label, "runtime" label is required format "runtime=qingcloud,env=production" | Yes      |

  Response Elements

  | Parameter name | Type    | Description                             |
  | -------------- | ------- | --------------------------------------- |
  | action         | String  | the corresponding action                |
  | runtime_env_id | String  | id of runtime_env                       |

* DeleteRuntimeEnv

  Request Parameters

  | Parameter name | Type   | Description       | Required |
  | -------------- | ------ | ----------------- | -------- |
  | runtime_env_id | String | id of runtime_env | Yes      |

  Response Elements

  | Parameter name | Type    | Description                             |
  | -------------- | ------- | --------------------------------------- |
  | action         | String  | the corresponding action                |
  | runtime_env_id | String  | id of runtime_env                       |

* CreateRuntimeEnvCredential

  Request Parameters

  | Parameter name | Type   | Description                           | Required |
  | -------------- | ------ | ------------------------------------- | -------- |
  | name           | String | name of runtime env credential        | No       |
  | description    | String | description of runtime env credential | No       |
  | content        | Dict   | content of runtime env credential     | Yes      |

  Response Elements

  | Parameter name            | Type    | Description                             |
  | ------------------------- | ------- | --------------------------------------- |
  | action                    | String  | the corresponding action                |
  | runtime_env_credential_id | String  | id of runtime_env                       |

* DescribeRuntimeEnvCredentials

  Request Parameters

  | Parameter name             | Type    | Description                                         | Required |
  | -------------------------- | ------- | --------------------------------------------------- | -------- |
  | runtime_env_credential_ids | Array   | id of runtime env credentials                       | No       |
  | search_word                | String  | search keyword, support runtime_env credential name | No       |
  | limit   | Integer | size of one page, default 10 ,max 100 | No |
  | offset | Integer | data offset, default 0  | No |
  | verbose                    | Integer | if 1 returns verbose information                    | No       |
  | owner                      | String  | owner of runtime env credential                     | No       |
  | status                     | String | status of runtime_env                                | No       | 

  Response Elements

  | Parameter name             | Type    | Description                               |
  | -------------------------- | ------- | ----------------------------------------- |
  | action                     | String  | the corresponding action                  |
  | runtime_env_credential_set | Array   | JSON format runtime env credentials array |
  | total_count                | Integer | count of runtime env credentials set      |

  Response Item

  | Parameter name            | Type   | Description                                                  |
  | ------------------------- | ------ | ------------------------------------------------------------ |
  | runtime_env_credential_id | String | id of runtime_env_credential                                 |
  | name                      | String | name of runtime_env_credential                               |
  | description               | String | description of runtime_env_credential                        |
  | content                   | Dict   | content of runtime_env_credential                            |
  | owner                     | String | owner of runtime_env_credential                              |
  | runtime_env_ids               | Array   | array of attached runtime_env id, return this value when verbose = 1 |
  | status                     | String | status of runtime_env                                        |
  | create_time                | Timestamp | create_time of runtime_env                                        |
  | status_time                     | Timestamp | status_time of runtime_env                                        |

* ModifyRuntimeEnvCredential

  Request Parameters

  | Parameter name            | Type   | Description                           | Required |
  | ------------------------- | ------ | ------------------------------------- | -------- |
  | runtime_env_credential_id | String | id of runtime_env_credential          | Yes      |
  | name                      | String | name of runtime_env_credential        | No       |
  | description               | String | description of runtime_env_credential | No       |
  | content                   | String | content of runtime_env_credential     | No       |
  
  Response Elements

  | Parameter name            | Type    | Description                             |
  | ------------------------- | ------- | --------------------------------------- |
  | action                    | String  | the corresponding action                |
  | runtime_env_credential_id | String  | id of runtime_env_credential            |
  
* DeleteRuntimeEnvCredential

  Request Parameters

  | Parameter name            | Type   | Description                  | Required |
  | ------------------------- | ------ | ---------------------------- | -------- |
  | runtime_env_credential_id | String | id of runtime_env_credential | Yes      |

  Response Elements

  | Parameter name            | Type    | Description                             |
  | ------------------------- | ------- | --------------------------------------- |
  | action                    | String  | the corresponding action                |
  | runtime_env_credential_id | String  | id of runtime_env_credential            |
  
* AttachCredentialToRuntimeEnv

  Request Parameters

  | Parameter name            | Type   | Description                  | Required |
  | ------------------------- | ------ | ---------------------------- | -------- |
  | runtime_env_credential_id | String | id of runtime_env_credential | Yes      |
  | runtime_env_id            | String | id of runtime_env            | Yes      |
  
  Response Elements

  | Parameter name            | Type    | Description                             |
  | ------------------------- | ------- | --------------------------------------- |
  | action                    | String  | the corresponding action                |
  | runtime_env_credential_id | String | id of runtime_env_credential 
  | runtime_env_id            | String | id of runtime_env            |

* DetachCredentialFromRuntimeEnv

  Request Parameters

  | Parameter name            | Type   | Description                  | Required |
  | ------------------------- | ------ | ---------------------------- | -------- |
  | runtime_env_credential_id | String | id of runtime_env_credential | Yes      |
  | runtime_env_id            | String | id of runtime_env            | Yes      |
  
  Response Elements

  | Parameter name            | Type    | Description                             |
  | ------------------------- | ------- | --------------------------------------- |
  | action                    | String  | the corresponding action                |
  | runtime_env_credential_id | String | id of runtime_env_credential |
  | runtime_env_id            | String | id of runtime_env            |
