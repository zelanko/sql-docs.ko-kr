---
title: "부록-1 (MySQLToSQL) | Microsoft Docs"
ms.prod: sql-non-specified
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.technology:
- sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: 2d22766d-ff09-420d-ae7c-13b443e28bd0
caps.latest.revision: 10
author: Shamikg
ms.author: Shamikg
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 42367162a6420688252a45801aa759fc1fbfd6e7
ms.contentlocale: ko-kr
ms.lasthandoff: 08/02/2017

---
# <a name="appendix---1-mysqltosql"></a>부록-1 (MySQLToSQL)
SSMA 콘솔 명령줄 옵션의 빠른 보기:  
  
|Sl 합니다. 아니요.|스위치|필수 여부|인수를 전환 합니다.|허용 되는 값|  
|-----------|----------|-------------|-------------------|--------------------|  
|1.|-s/스크립트|예|scriptfile|유효한 XML 파일 이름입니다.<br /><br />콘솔 스크립트 정의 파일입니다.|  
|2|-v/변수|아니요|variablevaluefile|유효한 XML 파일 이름입니다.<br /><br />변수는 스크립트 파일 사용 되는 경우이 파일을 지정 해야 합니다.|  
|3|-c/serverconnection|아니요|serverconnectionfile|유효한 XML 파일 이름입니다.<br /><br />이 파일 서버 연결 정보를 포함합니다.|  
|4|-x / xmloutput|아니요|xmloutputfile|이 옵션은 XML 형식으로 콘솔 출력을 나타냅니다. 이 옵션을 지정 하지 않으면 기본 출력 텍스트 형태로 표시 됩니다.<br /><br />Xmloutputfile 지정 되지 않은 경우 XML 출력은 STDOUT으로 전송 됩니다.<br /><br />Xmloutputfile에 콘솔 출력을 XML 형식으로 기록 되는 파일의 이름입니다.|  
|5|-l/로그|아니요|logfile|올바른 파일 이름입니다.|  
|6|-e/projectenvironment|아니요|projectenvironmentfolder|SSMA 프로젝트 환경 파일이 포함 된 올바른 폴더 이름입니다.|  
|7|-p/securepassword|아니요|-a/추가 {< server_id > [, … n] &#124; 모든}-c &#124; serverconnection < 서버 연결 파일 > [-v &#124; 변수 < 변수 값 파일 >] [-o/덮어쓰기]<br /><br />또는<br /><br />-a/추가 {< server_id > [, … n] &#124; 모든} – s &#124; 스크립트 < 스크립트 파일 > [-v &#124; 변수 < 변수 값 파일 >] [-o/덮어쓰기]<br /><br />-r/제거 {< server_id > [, … n] &#124; 모든}<br /><br />-l/목록<br /><br />– e/내보내기 {< 서버 id > [, … n] &#124; 모든} < 암호화 암호-파일 ><br /><br />– i 가져오기 / {< 서버 id > [, … n] &#124; 모든} < 암호화 암호-파일 >|를 지정 하는 경우이 옵션 다른 옵션과 함께 사용할 수 없습니다.<br /><br />서버 id: {string} 서버에 대해 제공 된 고유 ID<br /><br />서버 연결 파일: 서버 정의 파일 (serverconnectionfile 또는 스크립트 파일).<br /><br />변수 값 파일: 변수 정의 파일이 며 서버 연결 파일에 사용 합니다.<br /><br />암호화 암호 – 파일: 서버 암호 파일 사용자 지정 암호를 사용 하 여 암호화 합니다.|  
|8|-?|아니요|해당 사항 없음|해당 사항 없음|  
  
## <a name="see-also"></a>참고 항목  
[SSMA 콘솔 (MySQL)를 실행합니다.](http://msdn.microsoft.com/en-us/e3e9f7e4-0619-4861-a202-3d5d39953b26)  
  

