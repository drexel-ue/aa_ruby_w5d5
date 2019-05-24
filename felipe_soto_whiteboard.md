## Partner A: White Boarding

## Sorts

### Binary Search

Write a method that binary searches an array for a target and returns its
index if found. Assume a sorted array.

NB: YOU MUST WRITE THIS RECURSIVELY (searching half of the array every time).
We will not give you points if you visit every element in the array every time
you search.

For example, given the array [1, 2, 3, 4], you should NOT be checking
1 first, then 2, then 3, then 4.

def bsearch(array, target)
    return nil if array.empty?

    mid_idx = array.length / 2

    case target <=> array[mid_idx]
        when -1
            bsearch(array.take(mid_idx), target)
        when 0
            mid_idx
        when 1
            right_bsearch = bsearch(array.drop(mid_idx + 1), target)
            right_bsearch.nil? ? nil : right_bsearch + 1 + mid_idx
        end
    end
end


## Monkey Patching

### my_each

Write a method that calls a passed block for each element of the array

### dups

Write an array method that returns a hash where the keys are any element
that appears in the array more than once, and the values are sorted arrays
of indices for those elements.

class Array

    def duped_indices

        element_indices_hash = Hash.new { |hash, k| hash[k] = [] }

        self.each_with_index do |ele, idx|
            element_indices_hash[ele] << idx
        end

        elements_indices_hash.select { |k, v| v.length > 1 }
    end




    def my_each(&prc)

        i = 0
        while i < self.length
            prc.call(self[i])

            i += 1
        end

        self
    end

end


## Recursion

### Factorials

Write a method that recursively finds the first `n` factorial numbers
and returns them. N! is the product of the numbers 1 to N.
Be aware that the first factorial number is 0!, which is defined
to equal 1. The 2nd factorial is 1!, the 3rd factorial is 2!, etc.

def factorial_array(n)
    return [1] if n == 1

    facs_array = factorial_array(n - 1)
    facs_array << (n - 1) * facs_array[-1]

    facs_array

end