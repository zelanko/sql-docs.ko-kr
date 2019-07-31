---
title: 이벤트 알림에 대한 대화 보안 구성 | Microsoft 문서
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- event notifications [SQL Server], security
ms.assetid: 12afbc84-2d2a-4452-935e-e1c70e8c53c1
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 488b1efd533f038914f2d0186e29e28622531f02
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68048899"
---
# <a name="configure-dialog-security-for-event-notifications"></a>이벤트 알림에 대한 대화 보안 구성
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  [!INCLUDE[ssSB](../../includes/sssb-md.md)] 대화 보안을 구성해야 합니다. 대화 보안은 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 의 높은 수준의 대화 보안 모델에 따라 수동으로 구성해야 합니다. 높은 수준의 보안 모델은 원격 서버와 주고 받는 메시지의 암호화 및 암호 해독을 가능하게 합니다. 이벤트 알림은 한 방향으로 전송되지만 오류와 같은 다른 메시지는 반대 방향으로도 반환됩니다.  
  
## <a name="configuring-dialog-security-for-event-notifications"></a>이벤트 알림에 대한 대화 보안 구성  
 다음 단계에서는 이벤트 알림에 대한 대화 보안을 구현하는 과정을 설명합니다. 이러한 단계에 포함된 동작은 원본 서버와 대상 서버 둘 다에서 수행해야 합니다. 원본 서버는 이벤트 알림이 생성되는 서버입니다. 대상 서버는 이벤트 알림 메시지를 받는 서버입니다. 다음 단계로 넘어가기 전에 원본 서버와 대상 서버 둘 다에 대해 각 단계의 동작을 완료해야 합니다.  
  
> [!IMPORTANT]  
>  모든 인증서는 유효한 시작 날짜와 만료 날짜를 사용하여 만들어야 합니다.  
  
 **1단계: TCP 포트 번호와 대상 서비스 이름을 설정합니다.**  
  
 원본 서버와 대상 서버가 메시지를 받을 TCP 포트를 설정합니다. 대상 서비스의 이름도 결정해야 합니다.  
  
 **2단계: 데이터베이스 수준 인증에 대한 암호화 및 인증서 공유를 구성합니다.**  
  
 원본 서버와 대상 서버 둘 다에서 다음 동작을 완료합니다.  
  
|원본 서버|대상 서버|  
|-------------------|-------------------|  
|이벤트 알림과 마스터 키를 보관할 데이터베이스를 선택하거나 만듭니다.|마스터 키를 보관할 데이터베이스를 선택하거나 만듭니다.|  
|원본 데이터베이스에 대한 마스터 키가 없으면 [마스터 키를 만듭니다](../../t-sql/statements/create-master-key-transact-sql.md). 해당 인증서를 보호하려면 원본 데이터베이스와 대상 데이터베이스에 모두 마스터 키가 필요합니다.|대상 데이터베이스에 대한 마스터 키가 없으면 마스터 키를 만듭니다.|  
|원본 데이터베이스에 대한[로그인](../../t-sql/statements/create-login-transact-sql.md) 및 해당 [사용자](../../t-sql/statements/create-user-transact-sql.md) 를 만듭니다.|대상 데이터베이스에 대한 로그인 및 해당 사용자를 만듭니다.|  
|원본 데이터베이스의 사용자가 소유하는[인증서를 만듭니다](../../t-sql/statements/create-certificate-transact-sql.md) .|대상 데이터베이스의 사용자가 소유하는 인증서를 만듭니다.|  
|대상 서버가 액세스할 수 있는 파일에[인증서를 백업합니다](../../t-sql/statements/backup-certificate-transact-sql.md) .|원본 서버가 액세스할 수 있는 파일에 인증서를 백업합니다.|  
|대상 데이터베이스의 사용자와 WITHOUT LOGIN을 지정하여[사용자를 만듭니다](../../t-sql/statements/create-user-transact-sql.md). 이 사용자는 백업 파일로부터 생성될 대상 데이터베이스 인증서를 소유하게 됩니다. 이 사용자는 다음 3단계에서 만드는 대상 데이터베이스 인증서를 소유하는 용도로만 사용되므로 사용자를 로그인에 매핑할 필요는 없습니다.|원본 데이터베이스의 사용자와 WITHOUT LOGIN을 지정하여 사용자를 만듭니다. 이 사용자는 백업 파일로부터 생성될 원본 데이터베이스 인증서를 소유하게 됩니다. 이 사용자는 다음 3단계에서 만드는 원본 데이터베이스 인증서를 소유하는 용도로만 사용되므로 사용자를 로그인에 매핑할 필요는 없습니다.|  
  
 **3단계: 데이터베이스 수준 인증에 대한 인증서를 공유하고 사용 권한을 부여합니다.**  
  
 원본 서버와 대상 서버 둘 다에서 다음 동작을 완료합니다.  
  
|원본 서버|대상 서버|  
|-------------------|-------------------|  
|대상 데이터베이스 사용자를 소유자로 지정하여 대상 인증서의 백업 파일로부터[인증서를 만듭니다](../../t-sql/statements/create-certificate-transact-sql.md) .|원본 데이터베이스 사용자를 소유자로 지정하여 원본 인증서의 백업 파일로부터 인증서를 만듭니다.|  
|원본 데이터베이스 사용자에게 이벤트 알림을 만들 수 있는[권한을 부여합니다](../../t-sql/statements/grant-transact-sql.md) . 이 사용 권한에 대한 자세한 내용은 [CREATE EVENT NOTIFICATION&#40;Transact-SQL&#41;](../../t-sql/statements/create-event-notification-transact-sql.md).|기존 이벤트 알림 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 계약의 대상 데이터베이스 사용자에게 REFERENCES 권한을 부여합니다. `https://schemas.microsoft.com/SQL/Notifications/PostEventNotification`|  
|대상 서비스에 대한[원격 서비스 바인딩을 만들고](../../t-sql/statements/create-remote-service-binding-transact-sql.md) 대상 데이터베이스 사용자의 자격 증명을 지정합니다. 원격 서비스 바인딩은 원본 데이터베이스 사용자가 소유한 인증서의 공개 키가 대상 서버로 전송되는 메시지를 인증하도록 합니다.|대상 데이터베이스 사용자에게 CREATE QUEUE, CREATE SERVICE 및 CREATE SCHEMA 권한을[부여합니다](../../t-sql/statements/grant-transact-sql.md) .|  
||대상 데이터베이스 사용자로 데이터베이스에 연결되어 있지 않으면 지금 연결합니다.|  
||이벤트 알림 메시지를 받을[큐를 만들고](../../t-sql/statements/create-queue-transact-sql.md) 메시지를 배달할 [서비스를 만듭니다](../../t-sql/statements/create-service-transact-sql.md) .|  
||원본 데이터베이스 사용자에게 대상 서비스에 대한[SEND 권한을 부여합니다](../../t-sql/statements/grant-transact-sql.md) .|  
|대상 서버에 원본 데이터베이스의 Service Broker 식별자를 제공합니다. 이 식별자는 **sys.databases** 카탈로그 뷰의 [service_broker_guid](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md) 열을 쿼리하면 얻을 수 있습니다. 서버 수준 이벤트 알림의 경우 **msdb**의 Service Broker 식별자를 사용합니다.|원본 서버에 대상 데이터베이스의 Service Broker 식별자를 제공합니다.|  
  
 **4단계: 경로를 만들고 서버 수준의 인증을 설정합니다.**  
  
 원본 서버와 대상 서버 둘 다에서 다음 동작을 완료합니다.  
  
|원본 서버|대상 서버|  
|-------------------|-------------------|  
|대상 서비스로의[경로를 만들고](../../t-sql/statements/create-route-transact-sql.md) 대상 데이터베이스의 Service Broker 식별자 및 합의된 TCP 포트 번호를 지정합니다.|원본 서비스로의 경로를 만들고 원본 데이터베이스의 Service Broker 식별자 및 합의된 TCP 포트 번호를 지정합니다. 원본 서비스를 지정하려면 다음과 같은 제공된 서비스를 사용합니다. `https://schemas.microsoft.com/SQL/Notifications/EventNotificationService`|  
|**master** 데이터베이스로 전환하여 서버 수준의 인증을 구성합니다.|**master** 데이터베이스로 전환하여 서버 수준의 인증을 구성합니다.|  
|**master** 데이터베이스에 대한 마스터 키가 없으면 [마스터 키를 만듭니다](../../t-sql/statements/create-master-key-transact-sql.md).|**master** 데이터베이스에 대한 마스터 키가 없으면 마스터 키를 만듭니다.|  
|데이터베이스를 인증하는[인증서를 만듭니다](../../t-sql/statements/create-certificate-transact-sql.md) .|데이터베이스를 인증하는 인증서를 만듭니다.|  
|대상 서버가 액세스할 수 있는 파일에[인증서를 백업합니다](../../t-sql/statements/backup-certificate-transact-sql.md) .|원본 서버가 액세스할 수 있는 파일에 인증서를 백업합니다.|  
|[엔드포인트를 만들고](../../t-sql/statements/create-endpoint-transact-sql.md)합의된 TCP 포트 번호, FOR SERVICE_BROKER(AUTHENTICATION = CERTIFICATE *certificate_name*) 및 인증하는 인증서의 이름을 지정합니다.|엔드포인트를 만들고 합의된 TCP 포트 번호, FOR SERVICE_BROKER(AUTHENTICATION = CERTIFICATE *certificate_name*) 및 인증하는 인증서의 이름을 지정합니다.|  
|[로그인을 만들고](../../t-sql/statements/create-login-transact-sql.md)대상 서버의 로그인을 지정합니다.|로그인을 만들고 원본 서버의 로그인을 지정합니다.|  
|대상 인증자 로그인에 엔드포인트에 대한[CONNECT 권한을 부여합니다](../../t-sql/statements/grant-transact-sql.md) .|원본 인증자 로그인에 엔드포인트에 대한 CONNECT 권한을 부여합니다.|  
|[사용자를 만들고](../../t-sql/statements/create-user-transact-sql.md)대상 인증자 로그인을 지정합니다.|사용자를 만들고 원본 인증자 로그인을 지정합니다.|  
  
 **5단계: 서버 수준의 인증에 대한 인증서를 공유하고 이벤트 알림을 만듭니다.**  
  
 원본 서버와 대상 서버 둘 다에서 다음 동작을 완료합니다.  
  
|원본 서버|대상 서버|  
|-------------------|-------------------|  
|대상 인증자 사용자를 소유자로 지정하여 대상 인증서의 백업 파일로부터[인증서를 만듭니다](../../t-sql/statements/create-certificate-transact-sql.md) .|원본 인증자 사용자를 소유자로 지정하여 원본 인증서의 백업 파일로부터 인증서를 만듭니다.|  
|이벤트 알림을 만들 원본 데이터베이스로 전환하고 원본 데이터베이스 사용자로 연결되어 있지 않으면 지금 연결합니다.|이벤트 알림 메시지를 받을 대상 데이터베이스로 전환합니다.|  
|[이벤트 알림을 만들고](../../t-sql/statements/create-event-notification-transact-sql.md)대상 데이터베이스의 Service Broker 식별자를 지정합니다.||  
  
## <a name="see-also"></a>참고 항목  
 [GRANT&#40;Transact-SQL&#41;](../../t-sql/statements/grant-transact-sql.md)   
 [BACKUP CERTIFICATE&#40;Transact-SQL&#41;](../../t-sql/statements/backup-certificate-transact-sql.md)   
 [sys.databases&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)   
 [암호화 계층](../../relational-databases/security/encryption/encryption-hierarchy.md)   
 [이벤트 알림 구현](../../relational-databases/service-broker/implement-event-notifications.md)   
 [CREATE MASTER KEY&#40;Transact-SQL&#41;](../../t-sql/statements/create-master-key-transact-sql.md)   
 [CREATE LOGIN &#40;Transact-SQL&#41;](../../t-sql/statements/create-login-transact-sql.md)   
 [CREATE USER&#40;Transact-SQL&#41;](../../t-sql/statements/create-user-transact-sql.md)   
 [CREATE CERTIFICATE&#40;Transact-SQL&#41;](../../t-sql/statements/create-certificate-transact-sql.md)   
 [CREATE REMOTE SERVICE BINDING&#40;Transact-SQL&#41;](../../t-sql/statements/create-remote-service-binding-transact-sql.md)   
 [GRANT&#40;Transact-SQL&#41;](../../t-sql/statements/grant-transact-sql.md)   
 [CREATE ROUTE&#40;Transact-SQL&#41;](../../t-sql/statements/create-route-transact-sql.md)   
 [CREATE QUEUE&#40;Transact-SQL&#41;](../../t-sql/statements/create-queue-transact-sql.md)   
 [CREATE SERVICE&#40;Transact-SQL&#41;](../../t-sql/statements/create-service-transact-sql.md)   
 [CREATE ENDPOINT&#40;Transact-SQL&#41;](../../t-sql/statements/create-endpoint-transact-sql.md)   
 [CREATE EVENT NOTIFICATION&#40;Transact-SQL&#41;](../../t-sql/statements/create-event-notification-transact-sql.md)  
  
  
