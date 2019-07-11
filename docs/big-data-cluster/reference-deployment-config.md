---
title: 배포 구성 파일 참조
titleSuffix: SQL Server big data clusters
description: 빅 데이터 클러스터 배포 구성 파일에 대 한 참조입니다.
author: mihaelablendea
ms.author: mihaelab
ms.reviewer: mikeray
manager: jroth
ms.date: 04/23/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: f0ddc730e677c70e0d25274ed1383ea6f9c21934
ms.sourcegitcommit: e0c55d919ff9cec233a7a14e72ba16799f4505b2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/10/2019
ms.locfileid: "67727549"
---
# <a name="deployment-configuration-file-reference-for-big-data-clusters"></a>빅 데이터 클러스터에 대 한 배포 구성 파일 참조

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

이 문서에서는 SQL Server 2019 빅 데이터 클러스터 배포 구성 파일의 구조를 설명 하는 JSON 파일을 제공 합니다.

> [!TIP]
> 실제 배포 구성 파일을 사용 하지 마세요. 지침에 따라 대신 합니다 [배포 가이드](deployment-guidance.md#configfile) 구성 파일을 사용 하는 방법에 대 한 합니다.

## <a name="deployment-configuration-file"></a>배포 구성 파일

구조 및 빅 데이터 클러스터 배포 구성 파일 설정에 대 한 참조로 다음 JSON 파일을 사용 합니다.

```json
{
  "metadata": {
    "kind": {
      "name": "Deployment type",
      "description": "The type of deployment - in this case a 'Cluster'. Do not change this value."
    },
    "name": {
      "name": "Cluster Name",
      "description": "SQL Server big data cluster name. This is also the name of the Kubernetes namespace to deploy SQLServer big data cluster into."
    }
  },
  "spec": {
    "controlPlane": {
      "spec": {
        "docker": {
          "registry": {
            "name": "Docker Registry",
            "description": "The private Docker registry where the images used to deploy the SQL Server big data cluster are stored."
          },
          "repository": {
            "name": "Docker Repository",
            "description": "The private Docker repository within the above registry where images used to deploy the big data cluster are stored."
          },
          "imageTag": {
            "name": "Docker Image Tag",
            "description": "The Docker image tag used for the Docker images used for deploying the SQL Server big data cluster."
          },
          "imagePullPolicy": {
            "name": "Docker Image Pull Policy",
            "description": "The Docker image pull policy."
          }
        },
        "storage": {
          "usePersistentVolume": {
            "name": "Kubernetes Persistent Volume Use",
            "description": "Set this value to `true` to use Kubernetes Persistent Volume Claims for storage. Also specify the className in this case. Set this value to `false` to use ephemeral host storage for non production deployments."
          },
          "className": {
            "name": "Kubernetes Storage Class",
            "description": "If usePersistentVolume is `true` this indicates the name of the Kubernetes Storage Class to use. You must pre-provision the storage class and the persistent volumes or you can use a built in storage class if the platform you are deploying provides this capability."
          },
          "accessMode": {
            "name": "Kubernetes Persistent Volume Access Mode",
            "description": "Access mode for the Persistent Volume. Default value is ReadWriteOnce."
          },
          "size": {
            "name": "Kubernetes Persistent Volume Claim Size",
            "description": "The size of each Persisted Volume Claim created. Default value is 10Gi."
          }
        },
        "endpoints": [
          {
            "name": {
              "name": "Controller Endpoint Name",
              "description": "Name of Kubernetes service created for controller endpoint."
            },
            "serviceType": {
              "name": "Controller Service Type",
              "description": "Kubernetes service type for controller service. Possible values are LoadBalancer or NodePort."
            },
            "port": {
              "name": "Controller Service Port",
              "description": "The TCP/IP port that the controller service listens on the public network."
            }
          },
          {
            "name": {
              "name": "Management Proxy Endpoint Name",
              "description": "Name of Kubernetes service created for management proxy endpoint."
            },
            "serviceType": {
              "name": "Management Proxy Service Type",
              "description": "Kubernetes service type for management proxy service. Possible values are LoadBalancer or NodePort."
            },
            "port": {
              "name": "Management Proxy Service Port",
              "description": "The TCP/IP port that proxy service listens on the public network. This is the port used for computing the portal URL."
            }
          },
          {
            "name": {
              "name": "App Proxy Endpoint Name",
              "description": "Name of Kubernetes service created for app proxy endpoint."
            },
            "serviceType": {
              "name": "App Proxy Service Type",
              "description": "Kubernetes service type for proxy service. Possible values are LoadBalancer or NodePort."
            },
            "port": {
              "name": "App Proxy Service Port",
              "description": "The TCP/IP port that proxy service listens on the public network."
            }
          },
          {
            "name": {
              "name": "Gateway Endpoint Name",
              "description": "Name of Kubernetes service created for gateway endpoint."
            },
            "serviceType": {
              "name": "Gateway Service Type",
              "description": "Kubernetes service type for gateway service. Possible values are LoadBalancer or NodePort."
            },
            "port": {
              "name": "Gateway Service Port",
              "description": "The TCP/IP port that gateway service listens on the public network."
            }
          }
        ]
      },
    "pools": [
      {
        "metadata": {
          "kind": {
            "name": "Deployment Type",
            "description": "The type of deployment - in this case a Pool"
          },
          "name": {
            "name": "Pool Name",
            "description": "The name of the pool. `Default` is only allowed value in current version."
          }
        },
        "spec": {
          "type": {
            "name": "Pool Type",
            "description": "Master"
          },
          "replicas": {
            "name": "Master Pool Replicas",
            "description": "The number of replicas you would like in Master pool"
          },
          "storage": {
            "usePersistentVolume": {
              "name": "Kubernetes Persistent Volume Use",
              "description": "Set this value to `true` to use Kubernetes Persistent Volume Claims for storage. Also specify the className in this case. Set this value to `false` to use ephemeral host storage for non production deployments."
            },
            "className": {
              "name": "Kubernetes Storage Class",
              "description": "If usePersistentVolume is `true` this indicates the name of the Kubernetes Storage Class to use. You must pre-provision the storage class and the persistent volumes or you can use a built in storage class if the platform you are deploying provides this capability."
            },
            "accessMode": {
              "name": "Kubernetes Persistent Volume Access Mode",
              "description": "Access mode for the Persistent Volume. Default value is ReadWriteOnce."
            },
            "size": {
              "name": "Kubernetes Persistent Volume Claim Size",
              "description": "The size of each Persisted Volume Claim created. Default value is 10Gi."
            }
          },
          "endpoints": [
            {
              "name": {
                "name": "Master Endpoint Name",
                "description": "Endpoint name of Master pool"
              },
              "serviceType": {
                "name": "Master Pool Endpoint Type",
                "description": "Endpoint type of Master Pool - NodePort"
              },
              "port": {
                "name": "Master Pool Port",
                "description": "The port for the master endpoint"
              }
            }
          ]
        },
        "hadoop": {
          "yarn": {
            "nodeManager": {
              "memory": {
                "name": "Yarn Node Manager Memory",
                "description": "The standard memory is 18432"
              },
              "vcores": {
                "name": "Yarn Node Manager Virtual Cores",
                "description": "The standard virtual cores is 6"
              }
            },
            "schedulerMax": {
              "memory": {
                "name": "Yarn Scheduler Max Memory",
                "description": "The standard memory is 18432"
              },
              "vcores": {
                "name": "Yarn Scheduler Max Virtual Cores",
                "description": "The standard virtual cores is 6"
              }
            },
            "capacityScheduler": {
              "maxAmPercent": {
                "name": "Capacity Scheduler Max Percent",
                "description": "The standard max percentage is 0.3"
              }
            }
          },
          "spark": {
            "driverMemory": {
              "name": "Spark Driver Memory",
              "description": "The standard Spark driver memory is 2g"
            },
            "driverCores": {
              "name": "Spark Driver Cores",
              "description": "The standard Spark driverCores is 1"
            },
            "executorInstances": {
              "name": "Spark Executor Instances",
              "description": "The standard Spark executor instances is 3"
            },
            "executorMemory": {
              "name": "Spark Executor Memory",
              "description": "The standard Spark executor memory is 1536m"
            },
            "executorCores": {
              "name": "Spark Executor Cores",
              "description": "The standard Spark executor cores is 1"
            }
          }
        }
      },
      {
        "metadata": {
          "kind": {
            "name": "Deployment Type",
            "description": "The type of deployment - in this case a Pool"
          },
          "name": {
            "name": "Pool Name",
            "description": "The name of the pool. `Default` is only allowed value in current version."
          }
        },
        "spec": {
          "type": {
            "name": "Pool Type",
            "description": "Compute"
          },
          "replicas": {
            "name": "Compute Pool Replicas",
            "description": "The number of replicas you would like in Compute pool"
          },
          "storage": {
            "usePersistentVolume": {
              "name": "Kubernetes Persistent Volume Use",
              "description": "Set this value to `true` to use Kubernetes Persistent Volume Claims for storage. Also specify the className in this case. Set this value to `false` to use ephemeral host storage for non production deployments."
            },
            "className": {
              "name": "Kubernetes Storage Class",
              "description": "If usePersistentVolume is `true` this indicates the name of the Kubernetes Storage Class to use. You must pre-provision the storage class and the persistent volumes or you can use a built in storage class if the platform you are deploying provides this capability."
            },
            "accessMode": {
              "name": "Kubernetes Persistent Volume Access Mode",
              "description": "Access mode for the Persistent Volume. Default value is ReadWriteOnce."
            },
            "size": {
              "name": "Kubernetes Persistent Volume Claim Size",
              "description": "The size of each Persisted Volume Claim created. Default value is 10Gi."
            }
          }
        }
      },
      {
        "metadata": {
          "kind": {
            "name": "Deployment Type",
            "description": "The type of deployment - in this case a Pool"
          },
          "name": {
            "name": "Pool Name",
            "description": "The name of the pool. `Default` is only allowed value in current version."
          }
        },
        "spec": {
          "type": {
            "name": "Pool Type",
            "description": "Data"
          },
          "replicas": {
            "name": "Data Pool Replicas",
            "description": "The number of replicas you would like in Data pool"
          },
          "storage": {
            "usePersistentVolume": {
              "name": "Kubernetes Persistent Volume Use",
              "description": "Set this value to `true` to use Kubernetes Persistent Volume Claims for storage. Also specify the className in this case. Set this value to `false` to use ephemeral host storage for non production deployments."
            },
            "className": {
              "name": "Kubernetes Storage Class",
              "description": "If usePersistentVolume is `true` this indicates the name of the Kubernetes Storage Class to use. You must pre-provision the storage class and the persistent volumes or you can use a built in storage class if the platform you are deploying provides this capability."
            },
            "accessMode": {
              "name": "Kubernetes Persistent Volume Access Mode",
              "description": "Access mode for the Persistent Volume. Default value is ReadWriteOnce."
            },
            "size": {
              "name": "Kubernetes Persistent Volume Claim Size",
              "description": "The size of each Persisted Volume Claim created. Default value is 10Gi."
            }
          }
        }
      },
      {
        "metadata": {
          "kind": {
            "name": "Deployment Type",
            "description": "The type of deployment - in this case a Pool"
          },
          "name": {
            "name": "Pool Name",
            "description": "The name of the pool. `Default` is only allowed value in current version."
          }
        },
        "spec": {
          "type": {
            "name": "Pool Type",
            "description": "Storage"
          },
          "replicas": {
            "name": "Storage Pool Replicas",
            "description": "The number of replicas you would like in Storage pool"
          },
          "storage": {
            "usePersistentVolume": {
              "name": "Kubernetes Persistent Volume Use",
              "description": "Set this value to `true` to use Kubernetes Persistent Volume Claims for storage. Also specify the className in this case. Set this value to `false` to use ephemeral host storage for non production deployments."
            },
            "className": {
              "name": "Kubernetes Storage Class",
              "description": "If usePersistentVolume is `true` this indicates the name of the Kubernetes Storage Class to use. You must pre-provision the storage class and the persistent volumes or you can use a built in storage class if the platform you are deploying provides this capability."
            },
            "accessMode": {
              "name": "Kubernetes Persistent Volume Access Mode",
              "description": "Access mode for the Persistent Volume. Default value is ReadWriteOnce."
            },
            "size": {
              "name": "Kubernetes Persistent Volume Claim Size",
              "description": "The size of each Persisted Volume Claim created. Default value is 10Gi."
            }
          }
        },
        "namenode": {
          "replicas": {
            "name": "Hadoop Replicas",
            "description": "The number of replicas for hadoop"
          },
          "spec": {
            "storage": {
              "usePersistentVolume": {
                "name": "Kubernetes Persistent Volume Use",
                "description": "Set this value to `true` to use Kubernetes Persistent Volume Claims for storage. Also specify the className in this case. Set this value to `false` to use ephemeral host storage for non production deployments."
              },
              "className": {
                "name": "Kubernetes Storage Class",
                "description": "If usePersistentVolume is `true` this indicates the name of the Kubernetes Storage Class to use. You must pre-provision the storage class and the persistent volumes or you can use a built in storage class if the platform you are deploying provides this capability."
              },
              "accessMode": {
                "name": "Kubernetes Persistent Volume Access Mode",
                "description": "Access mode for the Persistent Volume. Default value is ReadWriteOnce."
              },
              "size": {
                "name": "Kubernetes Persistent Volume Claim Size",
                "description": "The size of each Persisted Volume Claim created. Default value is 10Gi."
              }
            }
          }
        },
        "hadoop": {
          "yarn": {
            "nodeManager": {
              "memory": {
                "name": "Yarn Node Manager Memory",
                "description": "The standard memory is 18432"
              },
              "vcores": {
                "name": "Yarn Node Manager Virtual Cores",
                "description": "The standard virtual cores is 6"
              }
            },
            "schedulerMax": {
              "memory": {
                "name": "Yarn Scheduler Max Memory",
                "description": "The standard memory is 18432"
              },
              "vcores": {
                "name": "Yarn Scheduler Max Virtual Cores",
                "description": "The standard virtual cores is 6"
              }
            },
            "capacityScheduler": {
              "maxAmPercent": {
                "name": "Capacity Scheduler Max Percent",
                "description": "The standard max percentage is 0.3"
              }
            }
          },
          "spark": {
            "driverMemory": {
              "name": "Spark Driver Memory",
              "description": "The standard Spark driver memory is 2g"
            },
            "driverCores": {
              "name": "Spark Driver Cores",
              "description": "The standard Spark driverCores is 1"
            },
            "executorInstances": {
              "name": "Spark Executor Instances",
              "description": "The standard Spark executor instances is 3"
            },
            "executorMemory": {
              "name": "Spark Executor Memory",
              "description": "The standard Spark executor memory is 1536m"
            },
            "executorCores": {
              "name": "Spark Executor Cores",
              "description": "The standard Spark executor cores is 1"
            }
          }
        }
      }
    ]
  }
}
```

## <a name="next-steps"></a>다음 단계

사용 하 여 배포 구성 파일 사용자 지정 하는 방법에 대 한 자세한 내용은 참조 하세요. [빅 데이터를 SQL Server를 배포 하는 방법에서 kubernetes 클러스터](deployment-guidance.md#configfile)합니다.
