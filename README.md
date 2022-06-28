# 1_grupa_raimonds_krauklis_terraform_project
Task:4
Uzdevumi
1.	Iekš GitHub.com izveidot jaunu repozitoriju ar nosaukumu {$grupas_nr}-grupa-{$vards}-{$uzvards)-terraform-project, piemēram, 4-grupa-janis-sniegs-terraform-project. 
2.	Noklonēt izveidoto repozitoriju uz lokālās darbstacijas, izmantojot git clone <url> komandu.
3.	Iekš repozitorija izveidot vidēja lieluma Terraform projekta struktūru, balstoties uz Terraform standarta moduļa struktūru, kā arī Terraform labajām praksēm, t.i., atseviški izveidot direktoriju priekš moduļiem un servisiem. Papildus servisa direktoriju iedalīt vairākas apakšdirektorijās, kas atspoguļotu atsevišķas izstrādes vides – dev, stage un prod.
4.	Izveidot “nginx-web-server” servisa apakšdirektorijas dev un stage vides direktorijās, piem., /services/dev/nginx-web-server, /services/stage/nginx-web-server.
5.	Izveidot EC2 un VPC moduļus iekš /modules/ec2/… un /modules/vpc/…, kuri pēc tam tiktu izsaukti “nginx-web-server” servisa Terraform konfigurācijas failā main.tf.
a.	Izveidot VPC (aws_vpc) ar 2 publiskiem un 2 privātiem apakštīkliem (aws_subnet).
b.	Izveidot interneta vārteju (IGW/aws_internet_gateway) un savienot to ar publisko maršutēšanas tabulu.
c.	Izveidot elastīgo IP adresi (EIP/aws_eip) iekš VPC.
d.	Izveidot tīkla adrešu translētāju (NAT/aws_nat_gateway) un izvietot to iekš publiskā subnet (subnet_id) un asociēt to ar pirmīt izveidotot EIP (allocation_id).
e.	Izveidot divas atsevišķas maršrutēšanas tabulas (aws_route_table) – vienu publisko tabulu un otru privāto:
i.	Publiskajā tabulā izveidot route, kurā cidr_block = “0.0.0.0/0” un gateway_id = IGW. Papildus asociēt (aws_route_table_association) publisko tabulu ar publisko subnet.
ii.	Privātajā tabulā izveidot route, kurā cidr_block = “0.0.0.0/0” un gateway_id = NAT. Papildus asociēt (aws_route_table_association) privāto tabulu ar privāto subnet.
f.	Izveidot vienu drošības grupu (SG/aws_security_group) zem izveidotā VPC, kura atļautu ienākošo trafiku (ingress) uz HTTP (80), HTTPS (443) un SSH (22) portiem.
i.	HTTP un HTTPS vajadzētu atļaut saņemt trafiku no 0.0.0.0/0.
ii.	SSH vajadzētu atļaut saņemt trafiku tikai no Jūsu IP adreses (noskaidrojiet kāda ir Jūsu IP adrese - https://www.myip.com/).
g.	Izmantojot Ubuntu 20.04 LTS AMI (aws_ami), izveidot EC2 (aws_instance) resursu iekš pirmīt izveidotā VPC publiskajā apakštīklā, kuram būtu piekļuve Internetam caur publiskās maršrutēšanas tabulu, kura ir asociēta ar interneta vārteju.
h.	Pielietot user_data argumentu iekš aws_instance resursa, uzstādīt Nginx ievietojot nepieciešamās komandas, pamatojoties uz Nginx konfigurācijas dokumentāciju.
6.	Kad EC2 un VPC moduļi ir izveidoti, uztaisīt /services/{$vide}/nginx-web-server servisa konfigurāciju, iekļaujot tādus failus kā main.tf, outputs.tf, variables.tf un terraform.tfvars.
a.	Atkarībā no vides, pamainīt mainīgās vērtības iekš terraform.tfvars tā, lai dev vidē instance_type ir t3.micro, bet stage vidē instance_type ir t3.medium.
7.	Izveidot jaunas pieprasījuma izmaiņas (pull request) uz GitHub attālinātā repozitorija, veicot nepieciešamās git darbplūsmas komandas, t.i., git add, git commit, git push utt.
a.	Mēģiniet veidot pēc iespējas biežak git commit un sūtīt izmaiņas uz attālināto repozitoriju, papildus norādot īsus un skaidrus komentārus par veiktajām izmaiņām.
b.	Iekš GitHub.com repozitorija pull request pierakstiet sev nepieciešamos komentārus par savu izstrādes gaitu. Piemēram, ar kādām problēmām saskaraties u.tml.
8.	Kad gan moduļu, gan servisa konfigurācijas faili ir izveidoti, palaist Terraform darbplūsmu:
a.	Iekš termināļa atvērt /services/{$vide}/nginx-web-server
b.	Palaist terraform init komandu, lai inicializētu projektu, lejupielādējot aws provaideri un main.tf konfigurācijas failā izsauktos moduļus (EC2 un VPC).
c.	Palaist terraform plan -var-file=terraform.tfvars komandu, lai apskatītu izmaiņas, kādas veiks Terraform, balstoties uz konfigurācijas failiem.
i.	Kārtīgi pārliecinieties, vai konfigurācijas failos nav pieļautas kļūdas.
d.	Palaist terraform apply -var-file=terraform.tfvars komandu, lai veiktu izmaiņas infrastruktūras konfigurācijā.
i.	Ja uzrāda kļūdas, tad pielietojiet atkļūdošanas iespējas TF_LOG utt.
9.	Iekš repozitorija izveidot README.md failu un tajā aprakstīt Terraform projektu, t.i., kā projektu var uzstādīt, ko projekts satur utt.

Papilduzdevumi (*)
10.	Izveidot atsevišku moduli ar nosaukumu “init” un izveidot tajā S3 bucket resursu iekš main.tf faila.
11.	Pielietot izveidoto S3 bucket priekš Terraform state glabāšanas, t.i., Terraform backend = s3.
12.	Izveidot aws_iam_instance_profile priekš AWS Systems Manager (SSM), kurš savienotu EC2 ar SSM servisu, kurš piedāvā plašu spektru ar infrastruktūras automatizācijas un kontroles funkcijām.
 
