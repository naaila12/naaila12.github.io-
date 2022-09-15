<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">

    <link rel="stylesheet" href="style.css">
 
    <title>SPCE</title>
</head>
<body>

    <div class="wrapper">
      <div class="form_container">
		    <form id="User_form">
          <div class="heading">
            <h2>FORM VALIDATION</h2>
          </div>
          <div class="form_wrap">
				    <div class="form_item">
					    <label>Name </label>
					    <input type="text" class="input-box" id="name" name="name"required/>
					  </div>
			    </div>
				  <div class="form_wrap">
				    <div class="form_item">
					    <label>Email </label>
					    <input required type="email" class="input-box" id="email" name="email"required />
					  </div>
			    </div>
			    <div class="form_wrap">
				    <div class="form_item">
					    <label>Password</label>
					    <input type="password" class="input-box" id="password" name="password" required />
					  </div>
			    </div>
			    <div class="form_wrap">
				    <div class="form_item">
					    <label>Date of Birth</label>
					    <input type="date" class="input-box" id="dob" name="dob"required/>
					  </div>
			    </div>

			    <input type="checkbox" name="agree" id="acceptTerms" />
              <label class="checkbox">Accespt Terms & Conditions</label>

              <div class="btn">
                <button type="submit" class="button">Submit</button>
			        </div>
		  </form>
		</div>
	  </div>
      <div class="table_entry" id="form"></div>
  <script>

      let today = new Date();
      let dd = today.getDate();
      let mm = today.getMonth() + 1; //January is 0 so need to add 1 to make it 1!
      let yyyy = today.getFullYear();
      if (dd < 10) {
          dd = '0' + dd
      }
      if (mm < 10) {
          mm = '0' + mm
      }
      maxDate = yyyy - 18 + '-' + mm + '-' + dd;
      minDate = yyyy - 55 + '-' + mm + '-' + dd;
      document.getElementById("dob").setAttribute("min", minDate);
      document.getElementById("dob").setAttribute("max", maxDate);

      let userEntries = localStorage.getItem("form");
      if (userEntries) {
          userEntries = JSON.parse(userEntries);
      } else {
          userEntries = [];
      }

      const displayEntries = () => {
          const savedUserEntries = localStorage.getItem("form");
          let entries = "";
          if (savedUserEntries) {
              const parsedUserEntries = JSON.parse(savedUserEntries);
              entries = parsedUserEntries
                  .map((entry) => {
                      const name = `<td class='border px-4 py-2'>${entry.name}</td>`;
                      const email = `<td class='border px-4 py-2'>${entry.email}</td>`;
                      const password = `<td class='border px-4 py-2'>${entry.password}</td>`;
                      const dob = `<td class='border px-4 py-2'>${entry.dob}</td>`;
                      const acceptTerms = `<td class='border px-4 py-2'>${entry.acceptTermsAndConditions}</td>`;
                      const row = `<tr>${name} ${email} ${password} ${dob} ${acceptTerms}</tr>`;
                      return row;
                  })
                  .join("\n");
          }
          var table = `<table class="table-auto w-full"><tr>
        <th class="px-4 py-2">Name</th>
        <th class="px-4 py-2">Email</th>
        <th class="px-4 py-2">Password</th>
        <th class="px-4 py-2">Dob</th>
        <th class="px-4 py-2">Accepted terms?</th>
      </tr>${entries} </table>`;
          let details = document.getElementById("form");
          details.innerHTML = table;
      };

      const saveUserForm = (event) => {
          event.preventDefault();
          event.preventDefault();
          const name = document.getElementById("name").value;
          const email = document.getElementById("email").value;
          const password = document.getElementById("password").value;
          const dob = document.getElementById("dob").value;
          const acceptTermsAndConditions =
              document.getElementById("acceptTerms").checked;
          const userDetails = {
              name,
              email,
              password,
              dob,
              acceptTermsAndConditions,
          };
          userEntries.push(userDetails);
          localStorage.setItem("form", JSON.stringify(userEntries));

          displayEntries(); // Add this line
      };

      let form = document.getElementById("User_form");
      form.addEventListener("submit", saveUserForm, true);
      displayEntries();

  </script>


</body>
</html>
