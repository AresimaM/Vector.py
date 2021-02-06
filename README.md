#------------------------------------------------------------------------------
# Vector.py
#------------------------------------------------------------------------------
"""
This module provides functions to perform standard vector operations.  Vectors
are represented as tuples of numbers (floats or ints).  Functions that take two 
vector arguments will raise a ValueError() exception if the two vectors are of
different dimensions.  
"""
#------------------------------------------------------------------------------
# import library modules
#------------------------------------------------------------------------------
import math 
import random 
#------------------------------------------------------------------------------
# function definitions
#------------------------------------------------------------------------------


# add() -----------------------------------------------------------------------
def add(u, v):
    """
    Return the vector sum u+v.
    """
    if len(u) != len(v): 
      raise ValueError('incompatible vectors: '+str(u)+', '+str(v)) 
    L = []
    for i in range(len(u)):
      #i = (u[i] + v[i]) 
      L.append(u[i]+v[i])
    T = tuple(L) 
    return T  
# end add() -------------------------------------------------------------------


# negate() --------------------------------------------------------------------
def negate(u):
    """
    Return the negative of the vector u.
    """    
   # return(i*-i for i in u) 
    L = []
    for i in u:
      L.append(-i) 
    T = tuple(L)
    return T
# end negate() ----------------------------------------------------------------   


# sub() -----------------------------------------------------------------------
def sub(u,v):
    """
    Return the vector difference u-v.
    """
    if len(u) != len(v): 
      raise ValueError('incompatible vectors: '+str(u)+', '+str(v))     
    return add(u,negate(v))
# end sub() -------------------------------------------------------------------


# scalarMult() ----------------------------------------------------------------
def scalarMult(c, u):
    """
    Return the scalar product cu of the number c by the vector u.
    """ 
    L = []
    for i in u: 
      L.append(i*c) 
    T = tuple(L)
    return T
# end scalarMult() ------------------------------------------------------------


# hadamard() ------------------------------------------------------------------
def hadamard(u, v): 
    """
    Return the Hadamard product of u with v.
    """ 
    if len(u) != len(v): 
      raise ValueError('incompatible vectors: '+str(u)+', '+str(v)) 
    L = []
    for i in range(len(u)):
      L.append(u[i]*v[i])
    T = tuple(L)
    return T 
# end hadamard() --------------------------------------------------------------


# dot() -----------------------------------------------------------------------
def dot(u,v):
    """
    Return the dot product of u with v.
    """ 
    return sum(hadamard(u,v)) 
# end dot() -------------------------------------------------------------------


# length() --------------------------------------------------------------------
def length(u):
    """
    Return the (geometric) length of the vector u.
    """ 
    a = dot(u,u)
    if a < 0:
      return math.sqrt(negate(a))
    else:
      return math.sqrt(a)
# end length() ----------------------------------------------------------------


# dim() -----------------------------------------------------------------------
def dim(u):
    """
    Return the dimension of the vector u.
    """ 
    return len(u)
# end dim() -------------------------------------------------------------------


# unit() ----------------------------------------------------------------------
def unit(v):
    """
    Return a unit (geometric length 1) vector in the direction of v.
    """ 
    a = 1/length(v)
    L = []    
    for i in v:
      L.append(i*a)
    T = tuple(L) 
    return T 
# end unit() ------------------------------------------------------------------


# angle() ---------------------------------------------------------------------
def angle(u,v):
    """
    Return the angle (in radians) between vectors u and v.
    """ 
    if len(u) != len(v): 
      raise ValueError('incompatible vectors: '+str(u)+', '+str(v)) 
    return math.acos(dot(unit(u),unit(v)))
# end angle() -----------------------------------------------------------------


# randVector() ----------------------------------------------------------------
def randVector(n,a,b):
    """
    Return a vector of dimension n whose components are random floats in
    the range [a, b).
    """ 
    L = [] 
    for i in range(n): 
       i = random.uniform(a,b)
       L.append(i)
    T = tuple(L)
    return T #could've just done return tuple(L)
# end randomVector() ----------------------------------------------------------
