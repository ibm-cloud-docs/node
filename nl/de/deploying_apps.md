---

copyright:
  years: 2018
lastupdated: "2018-08-15"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:tip: .tip}

# Node.js-Apps bereitstellen und integrieren
{: #deploy_apps}

Sie können Ihre Node.js-Apps mit einer Toolchain oder über die Befehlszeilenschnittstelle bereitstellen. Eine Toolchain ist eine Gruppe von Toolintegrationen. Die Befehlszeilenschnittstelle bietet eine einfache Möglichkeit, Ihre Apps und Serviceinstanzen bereitzustellen.

Weitere Informationen finden Sie in [Apps bereitstellen](../apps/dep-app-tool.html).

## Serverunabhängige Node.js-Apps bereitstellen
{: #serverless}

Um die serverunabhängige Entwicklung zu vereinfachen, können Sie das IBM Functions as a Service-Angebot (FaaS) {{site.data.keyword.openwhisk}} verwenden. {{site.data.keyword.openwhisk_short}} ermöglicht die Ausführung von Anwendungslogik als Reaktion auf Ereignisse oder direkte Aufrufe von Web- oder mobilen Apps über HTTP ohne die Bereitstellung oder Verwaltung von Servern.

{{site.data.keyword.openwhisk_short}} führt Systemverwaltungstasks wie automatische Skalierung, Verfügbarkeitsmanagement und Wartung aus, wodurch sich Entwickler auf das Schreiben von Anwendungslogik konzentrieren können.

Weitere Informationen finden Sie in [Serverunabhängige Apps entwickeln](../apps/deploying/functions.html).

## Back-End-Services mit einem generierten SDK integrieren
{: #backend_gensdk}

Mit dem {{site.data.keyword.IBM_notm}} SDK-Generator-Plug-in können Back-End-Services problemlos mit einem generierten SDK in Ihre App integriert werden. Wenn eine Änderung an einer REST-API vorgenommen wird, können Sie das SDK neu generieren und das alte SDK ersetzen, um ein nahtloses SDK-Upgrade durchführen zu können. Sie können die Befehlszeilenschnittstelle (CLI) auch in eine DevOps-Pipeline integrieren und sicherstellen, dass das SDK jedes Mal, wenn die App erstellt wird, mit der API-Spezifikation konsistent ist.

Weitere Informationen finden Sie in [Back-End-Services mit einem generierten SDK integrieren](../apps/deploying/api_management.html).

## Bereitstellung in einem Kubernetes-Cluster
{: #deploy_kube}

Sie können erfahren, wie Sie den Kubernetes-Service von {{site.data.keyword.cloud_notm}} zur Bereitstellung einer containerisierten Node.js-App verwenden können, die Watson Tone Analyzer verwenden. Im vorliegenden Szenario verwendet eine fiktive PR-Firma den {{site.data.keyword.cloud_notm}}-Service, um ihre Pressemitteilungen zu analysieren und Feedback zum Ton ihrer Nachrichten zu erhalten. Weitere Informationen finden Sie im Lernprogramm zum [Bereitstellen von Apps in Clustern](../containers/cs_tutorials_apps.html).

## Bereitstellung auf einem virtuellen Server
{: #virtual_deploy}

Ein virtueller Service bietet einen höheren Grad an Transparenz, Vorhersagbarkeit und Automatisierung für alle Workloadtypen. Terraform wird verwendet, um Ihre Infrastruktur sicher und effizient zu erstellen, zu ändern und zu versionieren.

Weitere Informationen finden Sie in [Bereitstellung auf einem virtuellen Server](../apps/vsi-deploy.html).