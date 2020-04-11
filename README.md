# Tips - Linux Admin
### Yum erroring out with: "Invalid release/repo/arch combination" | Error: Failed to synchronize cache for repo 'AppStream'
	OS: CentOS 8
	Pkg: Yum/Dnf 
	Problem output:		
		# yum list
		CentOS-8.0 -AppStream	25  B/s |  38  B     00:01
		Error: Failed to synchronize cache for repo 'AppStream'
		
	Cause: When running with a release version not available at the configured default repo. Can happen when the repo maintainer has bumped up the release version at the default repository as per the repo config file in the host failing to update.
	
	workaround: 
		Update the local repo file with updated repo configuration file from the maintainer.
	
		# dnf update -y --releasever=8 --nobest
			# dnf update -y --releasever=8 --nobest
			CentOS-8 - AppStream                                            
			CentOS-8 - Base                                                 
			CentOS-8 - Extras                                               
			CentOS-8 - PowerTools                                           
			Docker CE Stable - x86_64                                       
			GlusterFS                                                       
			Kubernetes                                                      
			Dependencies resolved.   
			================================================================
			 Package                                                        
			================================================================
			Installing:                                                     
			 yum-utils                                                      
				 replacing  dnf-utils.noarch 4.0.2.2-3.el8                  
			Upgrading:                                                      
			 container-selinux
				....
				....
			Transaction Summary                                           
			==============================================================
			Install   11 Packages                                         
			Upgrade  227 Packages                                         
			Skip       1 Package                                          
																		  
			Total download size: 341 M                                    
			Downloading Packages:                                         
			(1/238): centos-gpg-keys-8.1-1.1911.0.9.el8.noarch.rpm        
			(2/238): centos-repos-8.1-1.1911.0.9.el8.x86_64.rpm           
			(3/238): grub2-tools-efi-2.02-78.el8_1.1.x86_64.rpm           
			(4/238): kernel-4.18.0-147.5.1.el8_1.x86_64.rpm               				



		
		Note: If required, below steps can also be useful prior to running a huge update while suffering repo cache issues.
		# yun clean all
		# rm -rfv /var/cache/dnf/
	