# openpitrix-runtime-env-interface-sepc

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
* CreateRuntimeEnvLabel
* DescribeRuntimeEnvLabels
* ModifyRuntimeEnvLabel
* DeleteRuntimeEnvLabel

## Operator create runtime_env 

1. select runtime qingcloud/kubernetes
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

  | Parameter name | Type   | Description                | Required |
  | -------------- | ------ | -------------------------- | -------- |
  | runtime        | String | runtime name of env        | Yes      |
  | name           | String | name of runtime_env        | Yes      |
  | description    | String | description of runtime_env | No       |
  | endpoint       | String | endpoint of runtime_env    | Yes      |
  | zone           | String | zone of runtime_env        | Yes      |
  | visibility     | String | visibility of runtime_env  | No       |
  | owner          | String | owner of runtime_env       | No       |
  
  Response Elements
  
  | Parameter name | Type    | Description                             |
  | -------------- | ------- | --------------------------------------- |
  | action         | String  | the corresponding action                |
  | ret_code       | Integer | 0 is successful, others are error codes |
  | runtime_env_id | String  | id of runtime_env                       |

* DescribeRuntimeEnvs

  Request Parameters

  | Parameter name | Type   | Description                                              | Required |
  | -------------- | ------ | -------------------------------------------------------- | -------- |
  | runtime      | String | runtime name of env                                      | No       |
  | search_word    | String | search keyword, support runtime_env name | No       |
  | status         | Array | status of runtime_envs                                  | No       |
  | runtime_env_label_ids | Array | id of runtime env labels | No |
  | runtime_env_ids | Array  | id of runtime_envs                                       | No       |
  | visibility     | String | visibility of runtime_envs                               | No       |
  | owners         | Array  | owner of runtime_envs                                   | No       |
  | page_size | Integer | size of one page, default 10 | No |
  | page_number | Integer | page number, default 1 | No |
  | verbose | Integer | if 1 returns verbose information | No |

  Response Elements

  | Parameter name  | Type    | Description                             |
  | --------------- | ------- | --------------------------------------- |
  | action          | String  | the corresponding action                |
  | ret_code        | Integer | 0 is successful, others are error codes |
  | runtime_env_set | Array   | JSON format runtime_env array           |
  | total_count     | Integer | count of runtime env set                |
  | total_pages     | Integer | page of runtime env set                 |
  | page_size       | Integer | page_size of runtime env set            |
  | current_page    | Integer | current page runtime env set            |

  Response Item

  | Parameter name             | Type   | Description                                                  |
  | -------------------------- | ------ | ------------------------------------------------------------ |
  | runtime_env_id             | String | id of runtime_env                                            |
  | runtime                    | String | runtime of runtime_env                                       |
  | name                       | String | name of runtime_env                                          |
  | description                | String | description of runtime_env                                   |
  | endpoint                   | String | endpoint of runtime_env                                      |
  | zone                       | String | zone of runtime_env                                          |
  | visibility                 | String | visbility of runtime_env                                     |
  | owner                      | String | owner of runtime_env                                         |
  | status                     | String | status of runtime_env                                        |
  | runtime_env_credential_ids | Array  | crendentials attached to runtime_env, return this value when verbose = 1 |
  | runtime_env_labels         | Array  | labels of runtime_env                                        |

  Response Item runtime_env_labels

  | Parameter name       | Type   | Description                |
  | -------------------- | ------ | -------------------------- |
  | runtime_env_label_id | String | id of runtime_env_label    |
  | label_key            | String | key of runtime_env_label   |
  | label_value          | String | value of runtime_env_label |

* ModifyRuntimeEnv

  Request Parameters

  | Parameter name | Type   | Description                | Required |
  | -------------- | ------ | -------------------------- | -------- |
  | runtime_env_id | String | id of runtime_env          | Yes      |
  | name           | String | name of runtime_env        | No       |
  | description    | String | description of runtime_env | No       |
  | visibility     | String | visibility of runtime_env  | No       |
  | owner          | String | owner of runtime_env       | No       |

  Response Elements

  | Parameter name | Type    | Description                             |
  | -------------- | ------- | --------------------------------------- |
  | action         | String  | the corresponding action                |
  | ret_code       | Integer | 0 is successful, others are error codes |
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
  | ret_code       | Integer | 0 is successful, others are error codes |
  | runtime_env_id | String  | id of runtime_env                       |

* CreateRuntimeEnvCredential

  Request Parameters

  | Parameter name | Type   | Description                           | Required |
  | -------------- | ------ | ------------------------------------- | -------- |
  | name           | String | name of runtime env credential        | No       |
  | description    | String | description of runtime env credential | No       |
  | content        | Dict   | content of runtime env credential     | Yes      |
  | owner          | String | owner of runtime env credential       | No       |

  Response Elements

  | Parameter name            | Type    | Description                             |
  | ------------------------- | ------- | --------------------------------------- |
  | action                    | String  | the corresponding action                |
  | ret_code                  | Integer | 0 is successful, others are error codes |
  | runtime_env_credential_id | String  | id of runtime_env                       |

* DescribeRuntimeEnvCredentials

  Request Parameters

  | Parameter name             | Type    | Description                                         | Required |
  | -------------------------- | ------- | --------------------------------------------------- | -------- |
  | runtime_env_credential_ids | Array   | id of runtime env credentials                       | No       |
  | search_word                | String  | search keyword, support runtime_env credential name | No       |
  | owner                      | String  | owner of runtime env credential                     | No       |
  | page_size                  | Integer | size of one page, default 10                        | No       |
  | page_number                | Integer | page number, default 1                              | No       |
  | verbose                    | Integer | if 1 returns verbose information                    | No       |

  Response Elements

  | Parameter name             | Type    | Description                               |
  | -------------------------- | ------- | ----------------------------------------- |
  | action                     | String  | the corresponding action                  |
  | ret_code                   | Integer | 0 is successful, others are error codes   |
  | runtime_env_credential_set | Array   | JSON format runtime env credentials array |
  | total_count                | Integer | count of runtime env credentials set      |
  | total_pages                | Integer | page of runtime env credentials set       |
  | page_size                  | Integer | page_size of runtime env credentials set  |
  | current_page               | Integer | current page runtime env credentials set  |

  Response Item

  | Parameter name            | Type   | Description                                                  |
  | ------------------------- | ------ | ------------------------------------------------------------ |
  | runtime_env_credential_id | String | id of runtime_env_credential                                 |
  | name                      | String | name of runtime_env_credential                               |
  | description               | String | description of runtime_env_credential                        |
  | content                   | Dict   | content of runtime_env_credential                            |
  | owner                     | String | owner of runtime_env_credential                              |
  | runtime_env               | Dict   | infomation of attached runtime_env, return this value when verbose = 1 |

* ModifyRuntimeEnvCredential

  Request Parameters

  | Parameter name            | Type   | Description                           | Required |
  | ------------------------- | ------ | ------------------------------------- | -------- |
  | runtime_env_credential_id | String | id of runtime_env_credential          | Yes      |
  | name                      | String | name of runtime_env_credential        | No       |
  | description               | String | description of runtime_env_credential | No       |
  | content                   | String | content of runtime_env_credential     | No       |
  | owner                     | String | owner of runtime_env_credential       | No       |
  
  Response Elements

  | Parameter name            | Type    | Description                             |
  | ------------------------- | ------- | --------------------------------------- |
  | action                    | String  | the corresponding action                |
  | ret_code                  | Integer | 0 is successful, others are error codes |
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
  | ret_code                  | Integer | 0 is successful, others are error codes |
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
  | ret_code                  | Integer | 0 is successful, others are error codes |

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
  | ret_code                  | Integer | 0 is successful, others are error codes |
  
* CreateRuntimeEnvLabel

  Request Parameters

  | Parameter name            | Type   | Description                  | Required |
  | ------------------------- | ------ | ---------------------------- | -------- |
  | runtime_env_id            | String | id of runtime_env            | Yes      |
  | label_key                 | String | key of label                 | Yes      |
  | label_value               | String | value of label               | Yes      |
  
  
  Response Elements

  | Parameter name            | Type    | Description                             |
  | ------------------------- | ------- | --------------------------------------- |
  | action                    | String  | the corresponding action                |
  | ret_code                  | Integer | 0 is successful, others are error codes |
  | runtime_env_label_id      | String  | id of runtime_env_label                 |
  
* DescribeRuntimeEnvLabels

  Request Parameters

  | Parameter name        | Type    | Description                      | Required |
  | --------------------- | ------- | -------------------------------- | -------- |
  | runtime_env_labels    | Array   | runtime env labels               | No       |
  | runtime_env_id        | String  | id of runtime env                | No       |
  | page_size             | Integer | size of one page, default 10     | No       |
  | page_number           | Integer | page number, default 1           | No       |
  | verbose               | Integer | if 1 returns verbose information | No       |
  
  Request Item runtime_env_labels

  | Parameter name       | Type   | Description                |
  | -------------------- | ------ | -------------------------- |
  | runtime_env_label_id | String | id of runtime_env_label    |
  | label_key            | String | key of runtime_env_label   |
  | label_value          | String | value of runtime_env_label |

  Response Elements

  | Parameter name             | Type    | Description                               |
  | -------------------------- | ------- | ----------------------------------------- |
  | action                     | String  | the corresponding action                  |
  | ret_code                   | Integer | 0 is successful, others are error codes   |
  | runtime_env_label_set      | Array   | JSON format runtime env label array       |
  | total_count                | Integer | count of runtime env credentials set      |
  | total_pages                | Integer | page of runtime env credentials set       |
  | page_size                  | Integer | page_size of runtime env credentials set  |
  | current_page               | Integer | current page runtime env credentials set  |

  Response Item

  | Parameter name       | Type   | Description                                                  |
  | -------------------- | ------ | ------------------------------------------------------------ |
  | runtime_env_label_id | String | id of runtime_env_credential                                 |
  | label_key            | String | key of runtime_env_label                                     |
  | label_value          | String | value of runtime_env_credential                              |
  | runtime_env          | Dict   | infomation of attached runtime_env, return this value when verbose = 1 |

* ModifyRuntimeEnvLabel

  Request Parameters

  | Parameter name       | Type   | Description             | Required |
  | -------------------- | ------ | ----------------------- | -------- |
  | runtime_env_label_id | String | id of runtime_env_label | Yes      |
  | label_key            | String | key of label            | No       |
  | label_value          | String | value of label          | No       |
  
  
  Response Elements

  | Parameter name            | Type    | Description                             |
  | ------------------------- | ------- | --------------------------------------- |
  | action                    | String  | the corresponding action                |
  | ret_code                  | Integer | 0 is successful, others are error codes |
  | runtime_env_label_id      | String  | id of runtime_env_label                 |
  
* DeleteRuntimeEnvLabel

  Request Parameters

  | Parameter name            | Type   | Description                  | Required |
  | ------------------------- | ------ | ---------------------------- | -------- |
  | runtime_env_label_id      | String | id of runtime_env_label      | Yes      |
  
  
  Response Elements

  | Parameter name            | Type    | Description                             |
  | ------------------------- | ------- | --------------------------------------- |
  | action                    | String  | the corresponding action                |
  | ret_code                  | Integer | 0 is successful, others are error codes |
  | runtime_env_label_id      | String  | id of runtime_env_label                 |
  
