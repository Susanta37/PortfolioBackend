# PortfolioBackend


#in your front end submit data 
==================================================================
 const submitData = async (event) => {
    event.preventDefault();
    const { name, email, phone, feedback } = userData;
    if ( email  && feedback &&name && phone) {
      try {
        setLoading(true); // Set loading to true when submitting
        const res= await fetch(
          "http://localhost:8080/send-email",
          {
            method: "POST",
            headers: {
              "Content-Type": "application/json",
            },
            body: JSON.stringify(userData),
          }
        );
        console.log('res', res)
        if (res.ok) {
          toast.success("Thanks for your feedback!", {
            position: 'top-right',
            autoClose: 3000 // Specify the time in milliseconds (e.g., 3000ms = 3 seconds)
          });
          setUserData({
            name: "",
            email: "",
            phone: "",
            feedback: "",
          }); // Clear input fields
        } else {
          throw new Error("Failed to submit feedback");
        }
      } catch (error) {
        console.error("Error submitting feedback:", error);
        toast.error("Failed to submit feedback. Please try again later.", {
          position: 'top-right',
          autoClose: 3000 // Specify the time in milliseconds (e.g., 3000ms = 3 seconds)
        });
      }finally {
        setLoading(false); // Set loading back to false after submission
      }
    }
  };

  ===========================================================================
