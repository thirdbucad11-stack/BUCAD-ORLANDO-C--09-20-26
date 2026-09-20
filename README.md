C# MONOBEHAVIOR
//Concept: A game character represent as data + behavior (a class).
//CODE PROPER
using System;
class character
{
         public string Name;
		 public int X, Y;. //position on the map
		 public int Width, Height; //boungding shape
		 public int Health;
 
		 // Constructor: how a character is "born"
		 public Character(string name, int x, int y, int width, int height, int health)
        {
			Name = name
			X = x 
			Y = y 
			Width = width
			Height = Height
			Health = health
		}
    // behavior: methods define what the character can Do 
	     public void MoveTo(int bnewX, int newY)
		 {
		   X = newX;
		   Y = newY;
		   Console.WriteLine($"{name} move to ({X},{Y})");
		 }
         public void TakeDamage(int amount)
		 {
		   Health -= amount; // Decreased of your health
		   Health = Math.Max(Health , 0);
		   Console.WriteLine($"{Name} tool {amount} damage. Health:{Health}");
		 }
         public void PrintShape()
		 {
		   //Draw the character as an ASCII rectangle
		   for (int row = 0; row < Height' row++)	
		 {
           Console.WriteLine(new string('#', Width));
		 } 
    }
}
 
//Movement for Gridbased Character
class Program
{
  static void Main()
  {
       Character hero = new Character("Hero", 0, 0, 3, 2, 100);
	   hero:PrintShape();
	   hero,MoveTo(5 , 3);
	   hero.TakeDamage(25);
 
       }
}
// Grid BASE Movement
// GameObject
using UnityEngine;
public class GridMovement : Monobehaviour
{
        public float tileSize=1.0f; // size of one grid cell
		public float moveSpeed = 10f // how fast we glide between tiles(feel, not logic)
		public Vector3 targetPositionl
		private bool isMoving = false;
 
		void Start()
		{
          // Snap starting positon to the grid so everything lines up
        targetPosition = SnapToGrid(transform.position);
		transform.position =targetPosition
		}
		void Update(
		{
		  if(!isMoving);
		  {
		  HadleInput();
          }
		  else
		{
          //Smoothly guide to the next line
          transform.positon =Vector3.MoveTowards(transform.position,targetPosition.moveSpeed * Tile.deltaTime);
		  if (Vector 3.Distance(transform.position,targetPosition) <0.001f)
		  {
			transform.position = targetPosition;
			isMoving = false;
		  }       
     }
}
 
   void HadleInput()
{
	    Vector3 direction = Vector3.zero;
 
		if(Input.GetKeyDown(KeyCode.W)) direction = Vector3.up;
		else if(Input.GetKeyDown(KeyCode.S)) direction = Vector3.down;
		else if(Input.GetKeyDown(KeyCode.A)) direction = Vector3.left;
		else if(Input.GetKeyDown(KeyCode.D)) direction = Vector3.right;
 
		if (direction != Vector3.zero)
		{
			    targetPosition = transform.position + direction * tileSize;
				isMoving = true;
		{
		 return new Vector3(
                Mathf.Round(pos.x / tileSize) * tileSize,
				Mathf.Round(pos.y / tileSize) * tileSize,
				pos.z
		);
 
	  }
   }
//Movement for Freemovement Character
using UnityEngine;
public class Freemovement: MonoBehaviour
{
	    public float moveSpeed 5f;
 
		void update()
		{
		 // GetAxis give smooth values between -1 and 1
		 float horizontal = Input.GetAxis("Horizontal"); // A/D or LEFT/RIGHT ARROWS
		 float vertical = Input.GetAxis("Vertical"); // W/S or UP/DOWN ARROWS
		 Vector3 direction = new Vector3(horizontal, vertical, 0f);
		 // Diagonal Movement
		 if(direction.magnitude > 1f)
		{
			     direction.Normalize();
		}
		         transform.position += direction * moveSpeed * Time.deltaTime;
		}
    }
 
//Movement for Physicsbased Character
// GameObject/ Rigibody2D component
using UnityEngine;
 
[RequireComponent(typeif(Rigibody2D))]
public class PhysicsMovement: MonoBehaviour
{
       public float moveForce =f;
	   public float jumpForce = 7f;
	   public float maxSpeed = 6f;
 
	   private Rigibody2D rb;
	   private bool isGrounded = false;
 
	   void Start()
	   {
		       rb = GetComponent<Rigibody2D>();
	   } 
	   void FixedUpdate()
	   {
		//Physic Change FixedUpdate
		//frame rate 
		float horizontal = Input.GetAxis("Horizontal");
		rb.AddForce(new Vector2(horizontal * moveForce, 0f));
		// Clam Horizontal
		if(Mathf.Abs(rb.velocity.x)> maxSpeed);
		{
			    rb.velocity = new Vector2(Mathf.sign(rb.velocity.x)* maxSpeed, rb.velocity.y);
		}
	 }
	    void OnCollisionEnter2D(Collision2D colision)
		{
			    if (collision.gameObject.CompareTag("Ground"));
				{
					    isGrounded = true;
				}
		}
		void OnCollisionExit2D(Collision2D colision)
		{
			    if(colision.gameObject.CompareTag("Ground"))
				{
                         is Grounded = false;
		        }
		}
 
}
 
