----------------------------------------------RestmysqlDemoApplication-------------------------------------------------
package com.restmysql.restmysql_demo;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;

@SpringBootApplication
public class RestmysqlDemoApplication {

	public static void main(String[] args) {
		SpringApplication.run(RestmysqlDemoApplication.class, args);
	}
}
-----------------------------------------------Cloudvendor.java-------------------------------------------------

package com.restmysql.restmysql_demo;

import jakarta.persistence.Entity;
import jakarta.persistence.Id;

@Entity
public class Cloudvendor {

	@Id
	private String vendorId;
	private String vendorName;
	private String vendorAddress;
	private String vendorPhoneNumber;
	
	public Cloudvendor() {}
	
	public Cloudvendor(String vendorId, String vendorName, String vendorAddress, String vendorPhoneNumber) {
		super();
		this.vendorId = vendorId;
		this.vendorName = vendorName;
		this.vendorAddress = vendorAddress;
		this.vendorPhoneNumber = vendorPhoneNumber;
	}

	public String getVendorId() {
		return vendorId;
	}

	public void setVendorId(String vendorId) {
		this.vendorId = vendorId;
	}

	public String getVendorName() {
		return vendorName;
	}

	public void setVendorName(String vendorName) {
		this.vendorName = vendorName;
	}

	public String getVendorAddress() {
		return vendorAddress;
	}

	public void setVendorAddress(String vendorAddress) {
		this.vendorAddress = vendorAddress;
	}

	public String getVendorPhoneNumber() {
		return vendorPhoneNumber;
	}

	public void setVendorPhoneNumber(String vendorPhoneNumber) {
		this.vendorPhoneNumber = vendorPhoneNumber;
	}
}
-----------------------------------------------Cloudvendor_controller-------------------------------------------------

package com.restmysql.restmysql_demo;

import java.util.List;

import org.springframework.web.bind.annotation.DeleteMapping;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.PathVariable;
import org.springframework.web.bind.annotation.PostMapping;
import org.springframework.web.bind.annotation.PutMapping;
import org.springframework.web.bind.annotation.RequestBody;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RestController;

@RestController
@RequestMapping("/cloudvendor")
public class Cloudvendor_controller {
	
	Cloudvendor_service cloudvendor_service;
	
    public Cloudvendor_controller(Cloudvendor_service cloudvendor_service) {
		this.cloudvendor_service = cloudvendor_service;
	}

    
    ///Return specific vendor details
    
	@GetMapping("{vendorId}")
	public Cloudvendor getvendordetails(@PathVariable("vendorId")String vendorId)
	{
		return cloudvendor_service.getCloudvendor(vendorId);
		  
	}
	
	 ///Return all vendor details
	
	@GetMapping()
	public List<Cloudvendor> getvendordetails()
	{
		return cloudvendor_service.getCloudvendor();
		  
	}
	
	@PostMapping
	public String createvendordetails(@RequestBody Cloudvendor cloudvendor)
	{
		cloudvendor_service.createCloudvendor(cloudvendor);
		return "vendor infos created successfully" ;
	
	}
	
	@PutMapping
	public String updatevendordetails(@RequestBody Cloudvendor cloudvendor)
	{
		cloudvendor_service.updateCloudvendor(cloudvendor);
		return "vendor details updated" ;
		
	}
	
	@DeleteMapping("{vendorId}")
	public String deletedetails(@PathVariable String vendorId )
	{
		return cloudvendor_service.deleteCloudvendor(vendorId) ;
		
	}
}
-----------------------------------------------Cloudvendor_repository-------------------------------------------------
package com.restmysql.restmysql_demo;

import org.springframework.data.jpa.repository.JpaRepository;

public interface Cloudvendor_repository extends JpaRepository<Cloudvendor,String>{
}

----------------------------------------------Cloudvendor_service-------------------------------------------------

package com.restmysql.restmysql_demo;

import java.util.List;

public interface Cloudvendor_service {
	
	public String createCloudvendor(Cloudvendor cloudvendor);
	public String updateCloudvendor(Cloudvendor cloudvendor);
	public String deleteCloudvendor(String cloudvendorId);
	public Cloudvendor getCloudvendor(String cloudvendorId);
	public List<Cloudvendor> getCloudvendor();
}

----------------------------------------------Cloudvendor_implementaion-------------------------------------------------

package com.restmysql.restmysql_demo;

import java.util.List;

import org.springframework.stereotype.Service;

@Service
public class Cloudvendor_implementaion implements Cloudvendor_service {
	
	Cloudvendor_repository repository; ////to get data from database for that we need to instantiate it

	public Cloudvendor_implementaion(Cloudvendor_repository repository) {
		super();
		this.repository = repository;
	}
	
	@Override
	public String createCloudvendor(Cloudvendor cloudvendor) {
		// TODO Auto-generated method stub
		repository.save(cloudvendor);
		return "create success";
	}

	@Override
	public String updateCloudvendor(Cloudvendor cloudvendor) {
		// TODO Auto-generated method stub
		repository.save(cloudvendor);
		return "update success";
	}

	@Override
	public String deleteCloudvendor(String cloudvendorId) {
		// TODO Auto-generated method stub
		repository.deleteById(cloudvendorId);
		return "delete success";
	}

	@Override
	public Cloudvendor getCloudvendor(String cloudvendorId) {
		// TODO Auto-generated method stub
		return repository.findById(cloudvendorId).get();
		 
	}

	@Override
	public List<Cloudvendor> getCloudvendor() {
		// TODO Auto-generated method stub
		return repository.findAll();
	}
}



